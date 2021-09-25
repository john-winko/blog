---
layout: post
title:  "First Sprint"
date:   2021-09-18
categories: journey
---
A previous lesson learned is some .Net libraries do not have the expected or wanted functionality that you would expect.  I spent hours trying to debug why the [FileSystemWatcher]( https://docs.microsoft.com/en-us/dotnet/api/system.io.filesystemwatcher?view=net-5.0) would randomly not work (fire events). After some deep diving in Stack Overflow and some copious Google-Fu, I found out that if an application and some cases the OS such as windows 10 does not close the file or flush the file stream, the OS does not recognize any changes to a file or directory. In the case of Path of Exile, it maintains an open file stream to the Client.txt log file and nothing is signaled for changes in the FileSystemWatcher class.  Previously I solved this by creating an infinite loop:

# [Sprint 1 Commit](https://github.com/john-winko/PoeAcolyte/tree/5dffd278e0e12515d9fc7a154a3ef9d1107d5039)

~~~ csharp
private void InfiniteLoop(){
	while (true) {
		var currentPosition = _lastIndex
		using var file = File.Open(_filePath, FileMode.Open, FileAccess,Read, FileShare.ReadWrite);
		_lastIndex = file.Length - 1;
		
		If (_lastIndex <= currentPosition) continue;
		
		file.Position = currentPosition;
		using var reader = new StreamReader(file);
		
		while (!reader.EndOfStream)
		{
			ParseEntry(reader.ReadLine());
		}
	}
}
~~~

While this may still be the best option, I will try to maintain an open file stream to the client.txt file and check it on a 2 second interval.

~~~ csharp
private void TimerOnElapsed(object sender, ElapsedEventArgs e)
{
    if (_streamReader.EndOfStream) return;
    
    try
    {
        var changes = _streamReader.ReadToEnd();
        FileChanged?.Invoke(this, new FileChangedEventArgs(changes));
    }
    catch (Exception exception)
    {
        Console.WriteLine(exception);
    }
}
~~~

Another feature that had to be coded in was cross thread calls. Events fired on a non-UI thread cannot be invoked on a UI thread. To solve this without an overabundance of:

~~~ csharp
if (this.textBox1.InvokeRequired)
{ 
    SetTextCallback d = new SetTextCallback(SetText);
    this.Invoke(d, new object[] { text });
}
else
{
    this.textBox1.Text = text;
}
~~~

Thanks to u/RickardN on [Stack Overflow](https://stackoverflow.com/a/23265754) , I decided just to write an extension class:
 
~~~ csharp
public static class CrossThreadExtensions
{
    public static void PerformSafely(this Control target, Action action)
    {
        if (target.InvokeRequired)
        {
            target.Invoke(action);
        }
        else
        {
            action();
        }
    }
}
~~~

Now, all that must be done is create a lambda action:

~~~ csharp
_textBox.PerformSafely(() => _textBox.Text += text);
~~~

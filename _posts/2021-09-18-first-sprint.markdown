---
layout: post
title:  "First Sprint"
date:   2021-09-18
categories: journey
---
A previous lesson learned is some .Net libraries do not have the expected or wanted functionality that you would expect.  I spent hours trying to debug why the [FileSystemWatcher]( https://docs.microsoft.com/en-us/dotnet/api/system.io.filesystemwatcher?view=net-5.0) would randomly not work (fire events). After some deep diving in Stack Overflow and some copious Google-Fu, I found out that if an application and some cases the OS such as windows 10 does not close the file or flush the file stream, the OS does not recognize any changes to a file or directory. In the case of Path of Exile, it maintains an open file stream to the Client.txt log file and nothing is signaled for changes in the FileSystemWatcher class.  Previously I solved this by creating an infinite loop:

~~~ csharp
private void InfiniteLoop(){
	while (true) {
		var currentPosition = _lastIndex
		using var file = File.Open(_filePath, FileMode.Open, FileAccess,Read, FileShare.ReadWrite);
		_lastIndex = file.Length - 1;
		If (_lastIndex <= currentPosition) continue;
		file.Position = currentPosition;
		using var reader = new StreamReader(file);
		while (!reader.EndOfStream){
			ParseEntry(reader.ReadLine());
		}
	}
}
~~~

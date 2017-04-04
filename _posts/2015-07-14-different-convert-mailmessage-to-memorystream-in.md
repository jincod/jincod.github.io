---
title: Different convert MailMessage to MemoryStream in .NET4 and .NET4.5
tags: [.NET, MailMessage]
redirect_from: /post/124046088185
---
Method:

```csharp
private static MemoryStream ConvertMailMessageToMemoryStream(MailMessage message)
{
    Assembly assembly = typeof (SmtpClient).Assembly;
    Type mailWriterType = assembly.GetType("System.Net.Mail.MailWriter");
    var fileStream = new MemoryStream();
    ConstructorInfo mailWriterContructor =
        mailWriterType
            .GetConstructor(BindingFlags.Instance | BindingFlags.NonPublic, null, new[] {typeof (Stream)}, null);
    object mailWriter = mailWriterContructor.Invoke(new object[] {fileStream});
    MethodInfo sendMethod =
        typeof (MailMessage)
            .GetMethod("Send", BindingFlags.Instance | BindingFlags.NonPublic);
    sendMethod
        //.Invoke(message, BindingFlags.Instance | BindingFlags.NonPublic, null, new[] {mailWriter, true}, null);
        // for .net 4.5 user this:
        .Invoke(message, BindingFlags.Instance | BindingFlags.NonPublic, null, new[] {mailWriter, true, true}, null);
    MethodInfo closeMethod =
        mailWriter
            .GetType()
            .GetMethod("Close", BindingFlags.Instance | BindingFlags.NonPublic);
    closeMethod.Invoke(mailWriter, BindingFlags.Instance | BindingFlags.NonPublic, null, new object[] {}, null);
    return fileStream;
}
```

.NET4:

```csharp
sendMethod.Invoke(message, BindingFlags.Instance | BindingFlags.NonPublic, null, new[] {mailWriter, true}, null);
```

.NET4.5

```csharp
sendMethod.Invoke(message, BindingFlags.Instance | BindingFlags.NonPublic, null, new[] {mailWriter, true, true}, null);
```

Different:

```diff
-new[] {mailWriter, true}
+new[] {mailWriter, true, true}
```
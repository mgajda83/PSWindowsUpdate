# Issues
Since Issues has been disabled, and the source code is not available, and there is no other way to contact you, I will add this here.

## `Remove-WindowsUpdate` crash
The `Remove-WindowsUpdate` command crashes with error "Object reference not set to an instance of an object." if you use `-UpdateID` parameter.

I believe this is because it tries to update the `KBArticleID` property (to remove the "KB" prefix), even though it is null.

It is impossible to give `KBArticleID` a value when using the `-UpdateID` parameter, since it is on a different parameter set.

Decompiled sources:
```cs
namespace PSWindowsUpdate
{
  [Cmdlet("Remove", "WindowsUpdate", ConfirmImpact = ConfirmImpact.High, SupportsShouldProcess = true)]
  public class RemoveWindowsUpdate : PSCmdlet
  {
    ...
    private void CoreProcessing()
    {
      string invocationName = this.MyInvocation.InvocationName;
      string str1 = this.KBArticleID.Replace("KB", ""); // <-- here
      foreach (string str2 in this.ComputerName)
      {
      ...
```

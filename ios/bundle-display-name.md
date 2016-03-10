# Bundle Display Name

##### Source: `pain and suffering`

Somewhere around iOS 9, Apple introduced a new application property called "Bundle Display Name", and not to be confused with "Bundle Name" which is of course different. At any rate, it turns out that as of circa iOS 9.2.1, the absence of that property results in any permission requests (e.g. camera, location) not being shown. Instead, the request returns False, silently. So, kids, **[set your Bundle Display Names](http://stackoverflow.com/questions/34696761/avcapturedevice-requestaccessformediatype-never-pops-up-window-and-always-return)**.

As an aside, such a pain to debug this as it only manifests in release/testflight builds, and then only on devices that haven't previously granted the permissions. So, yeah, that was fun.
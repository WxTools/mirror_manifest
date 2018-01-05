# Android for MSM Project

Qcom BaseLine mirror from [codeaurora](https://source.codeaurora.org/quic/la)



## Using a local mirror

When using several clients, especially in situations where bandwidth is scarce, it is better to create a local mirror of the entire server content, and to sync clients from that mirror (which requires no network access). The download for a full mirror is smaller than the download of two clients, while containing more information.

These instructions assume that the mirror is created in /usr/local/aosp/mirror. The first step is to create and sync the mirror itself. Notice the --mirror flag, which can be specified only when creating a new client:

```
$ mkdir -p /usr/local/aosp/mirror
$ cd /usr/local/aosp/mirror
$ repo init -u https://github.com/WxTools/mirror_manifest.git -b codeaurora --mirror
$ repo sync
```
```
$ repo init -u ssh://git@github.com/WxTools/mirror_manifest.git -b codeaurora --mirror
```
Once the mirror is synced, new clients can be created from it. Note that it's important to specify an absolute path:

```
$ mkdir -p /usr/local/aosp/master
$ cd /usr/local/aosp/master
$ repo init -u /usr/local/aosp/mirror/platform/manifest.git
$ repo sync
```
Finally, to sync a client against the server, the mirror needs to be synced against the server, then the client against the mirror:

```
$ cd /usr/local/aosp/mirror
$ repo sync
$ cd /usr/local/aosp/master
$ repo sync
```
It's possible to store the mirror on a LAN server and to access it over NFS, SSH or Git. It's also possible to store it on a removable drive and to pass that drive around between users or between machines.


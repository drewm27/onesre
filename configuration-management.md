## Configuration Management

Configuration management is essential to an automated environment. I believe the choice of tool boils down to these features
1. The configuration management tool needs to be able to handle every single type of deployment environment including docker images, bare hardware and virtual machines. Only tools that don’t try to do everything and stick to the unix philosophy of small tools strung together can accomplish this goal. Generally the most flexible ones tend to focus on roles consisting of a tree of files and a preinstall and postinstall script.
2. The configuration management tool syntax needs to be easy enough for a Systems Administrator or Site Reliability Engineer to understand without additional training. This also prevents deployment errors and downtime due to lack of experience. That tends to narrow things down to the best language being bash.
3. Push vs pull: Doing push changes are inherently safer. Pull changes can’t be as easily canceled or rolled back due to the randomness of machine deployment. Also major services have to be rolled out with push in a sequential fashion anyway to give them enough time to restart, be tested and come up before the next instance is upgraded, otherwise major “everything is down” failures can happen.
4. Config file abstraction might be helpful for when you support a very operating system diverse environment, but as most corporations aspire to a very homogeneous environment, abstraction quickly leads to deployment errors because you cannot easily predict the final configuration files.
5. Simpler, easier to understand, easier to develop, easier to debug configuration management systems have less misunderstandings and code errors and will always create less downtime. Long debugging sessions = long outages.
The only one that satisfies all of the above goals is the one I’ve used quite a bit in the past. Here’s a link: <https://code.google.com/archive/p/slack/>

It is based on configuration management roles that consist of a tree of files, and a preinstall, fixfiles, and postinstall script written in bash, along with a single file for hostname to roles mapping. Throw it into git for versioning. It automatically backs up files that it overwrites, along with marking configuration managed files on the system read-only. It is based around rsync, so it’s very low bandwidth. The server portion is just an rsync daemon and tree of files organized into roles, and the client is just a fancy Perl wrapper around rsync. RPMs and DEBs clients already exist. It was written by a Google employee and is heavily used at Google. 
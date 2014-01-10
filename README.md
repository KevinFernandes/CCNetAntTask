CCNetAntTask
============

An AntTask plugin for Cruise Control .Net

CCNet has a NAnt task built in as part of its core but it does not have an Ant task.  This project attempts to remedy
that.  The source for the AntTask is taken directly from the NantTask in the CCnet Core library, so all credit for this 
task belongs to those great folks.

The modifications made to the NAntTask to allow it to run Ant jobs properly is in several areas:

1.  The parameter formating for NAnt uses a ":" between the flag the value, but Ant uses a simple space in some cases or no space at all in others.  So parameter formating was fixed where appropriate.
2.  By default the -nologo flag was set to true but Ant (at least the version I was using) does not have a -nologo flag, so this flag was removed from the output of parameters.
3.  The default logger and listener are not correct for Ant, the defaults are .Net classes but Ant wants Java classes instead.  I removed the default values but I have not tried any values at all so this area may not work as expected.
4.  There is an issue with the Parameter Formatter that CCNet uses when it formats the CCNet variables for Ant, I had to wrap the values in '' (quotes) in order to get them passed correctly.  For some reason the CCNet formatter outputs empty values and I think this causes Ant some issues.  This should be looked at further if you really need the CCNet variables.

Usage:
In your ccnet.config file you can use this just like you would use the NAnt task

``` XML
<ant>
  <executable>D:\apache-ant\bin\ant.bat</executable>
  <baseDirectory>D:\MyProject</baseDirectory>
  <buildArgs>-DprojectVersion=1.0.0</buildArgs>
  <description>Building MyProject Java code</description>
  <buildFile>build.xml</buildFile>
  <targetList>
    <target>release</target>
  </targetList>
</ant>
```

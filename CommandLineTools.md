The ten commandments of commandline tools
========================

1 - Thou tool shall indicate success by returning 0
-----
Simple, if the command worked, exit 0.  No need to print on stdout that it was all nice and it worked bueatifully.  Just exit 0

2 - Thou tool shall indicate failure by returning non-zero.
-----
Commandment 1 only works if commandment 2 is strictly adhered to.  if _ANYTHING_ did not work as expected
...  _ANYTHING_ ...  could be a fatal exception or just that the command was asked to find somehting and it could not.

failure to achieve a result, is indicated with a non-zero exit code.

Do not make your clients parse any text to figure out that something did not succeed.  Just return anything but 0.

Now if you need to be fancy... make that a signed return... negative means bad... exceptions, stuff that's outside 
the control of the tool itself that prevented it from functionning.  (missing config, no database, corrupted data files whatever.)

and popsitive means the command worked as intended and completed the command but could not get the results for whatever reason.
ex, a command that asks where something is...  when that something cant be found.

Many command will be expected to return _something_ of value to the caller.  When that something cant be returned for whatever reason
do not make your client think, do not make them parse useless values... in short... do not be rude to your client, just indicate your command 
failed to return expected value so no need to bother parsing the output.

3 - Thou shall reserve stdout for the output of the command used
------
This one looks obvious... and yet...

4 - Tough shall not adorn or decorate stdout unless the command explicitly calls for it
-----
One could paraphrase this rule to : Dont be rude !

Dont make your client parse the actual output from a sea of useless text.

The stdout should be reserved for the output of your command.  That output should be parseable _as is_ under the rules of your shell.
as such any adornment you might have added with your logging mechanism DO NOT BELONG on stdout.

Now some shell have their own rules, powershell for example allows the return of objects which it will format in the output.  
the output thus _looks_ like ot was adorned, but this was done _by the shell_  That very same command when piped to another command 
will not have these adornments.  So your command tool should not adorn the requested output either.

if you cant pipe the requested output raw then you are doing it wrong

5 - Tou shall define failure as failure for the stated command to perform it's task as it was explicitly called
-----
stated in commandment 2 but deserves it's own commandment.

Some justify the error code as strictly reserved for exception.  Cant find what you were looking for, the command "did it's job" 
so exit code 0... well...  no...

This basically means that the exit code becomes insuficient to know if the output needs to be interpreted, 
it now must _also_ be parsed for success.

This is rude.  the client of your commandline tool does not care about pointing fingers, the client cares that
the tool did what it's being asked of it.  Therefore if the command's code executed to the end but could not 
find the answers it was commanded to find... then this is... also a failure in the eye of the client.

Some here are often tempted to also include implicit failures.   for examplem a command that deletes somthing that
doe snot exist... well... the goal is to delete, to un-exist it... so if it's not there then success right ?

NO, expectation was that the thing was supposed to be there... it was not... so it effectively _failed_ to delete it.

the command is making a decision (see next commandment) to 

6 - Thou tool shall not make decision on it's own, aka ambiguity is another name for failure
-----

This is pretty broad.  In here fit the case from above where a delete command cant find the thing to delete.

Here there should be a flag to tell the command that this is a failure or not rather than _assume_ it to be ok.

Here fits also default parameters.  These should be neutral, any action should be taken _explicitly_ by the tool.

_Sometimes_ the default is so obvious that it can be safely assumed... but these cases are rare.. or should be rare.

say the dir command...  yes we can _assume_ that without an argument it means to use the current working directory to run...

but... this creates inconsistency with other command... should the deldir also assume current working directory ?

here basically default arguments, default config, cannot cause a command to _alter_ a system implicitly would be a good rule of thumb.

same goes for exeuction, we often arise in a situation where we can assume that this or that thus we will default to such behaviour...
this is wrong... if your command attempts to decide from information that is not _directly_ available in the parameters or that 
the analysis of the arguments would cause side effect form their intended purpose then best fail.

in short...  any ambiguity should be eliminated mercilesly.

7 - Thou shall reserve stderr for logs of the tool itself
-----
So stdout is for the command output...

then _EVERYTHING ELSE_ goes to stderr...

> yeah but it's called standard ERROR

I DONT CARE

if you start polluting stdout with information that is not strictly the desired command output then you ...

are being rude !

You want the output to be nice ? cool !  but not at the cost of me spending my time filtering the chaff from the wheat.
Your embelishement is disrespectfull to my time as a client of your tool.

be respectfull to the people using the tool, being nice to look at is never as important as being easy and obvious to use.

Now you want to be nice still...  well you can do so _explicitly_ with command switches to present the information in human readable way.
embelishment should be a opt-in not opt-out.

Logs however, all these little internal information strings from your app that help YOU (it's creator) figure out what's happening 
under the hood.  these ALWAYS belong to stderr so to guarantee stdout is ALWAYS left for the output of the command itself...
your command has no output... then stdout shows nothing

but your stderr can show stuff though.


8 - Thou tool shall have be helpfull in it's action, in it's help and in it's logs
-----

Ensure your app has a proper AND HELPFULL help menu.  listing the names of the options is NOT HELPFULL
tell me what do they do, what parameter they take, what to expect as output.  The CLI commands and their options 
is your API to the world, so document it.  Help here is these function headers in an interface declaration where 
people reading it do not have access to the implementation.

there are enough excellent cmd line tool to help extract this from code hints there is no good reason to neglect 
the help menu anymore.

the logs should be sparse and to the point.  For verboseness that's why you have debug and trace (if you dont have trace, you should)
the default log level should be to output _unadorned_ error and warning messages.  In short, the default log level is essentially no log
except when something goes wrong.

Adornment appear when the user _explicitly_ request more verbose logs either by aubmenting verboseness or by providing a log format / config directly

9 - Thou tool shall have readable output in any circumstances
-----
10 - Thou shall prefer named unordered arguments over positionnal ordered arguments
-----

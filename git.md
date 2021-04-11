**git checkout -b mybranch origin/abranch**
will create mybranch and track origin/abranch

**git checkout --track origin/abranch** 
will only create 'abranch', not a branch with a different name.

vscode içinde 
git commit yazarsak vim açılır.
i tuiuna bas input moduna geçecek
esc bas çıkar
:wq   tuşlarına bas save eder ve çıkar.



Because you pressed i to enter your text, I think that editor is vim. Assuming that you typed in your commit message ok, you have to do

<esc> :w <enter>
to write to the file and

<esc> :q <enter>
to quit. Note: things in <> denote key presses.

How to check the differences between local and github before the pull [duplicate]
https://stackoverflow.com/questions/6000919/how-to-check-the-differences-between-local-and-github-before-the-pull
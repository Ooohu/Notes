# Handy Tools
###### tags: `computing` `CheatSheet`
- [VIM](#VIM)
- [ROOT](#ROOT)
- [UNIX](#UNIX)
- [VNC](#VNC-remote-screen)
- [BASH](#BASH)

## VIM
`vimdiff <fileA.txt> <fileB.txt>`

Open 2 files with vertical split:
 `vim -O file1 file2` 

Open 2 files with horizontal split:
 `vim -o file1 file2` 
 
Only show lines contains the keyword:
```
:vimgrep <keyword> %
:cwindow
```

## TMUX
`tmux ls` shows sessions with IDs
`tmux attach-session -t #` bring back the # session.

## UNIX

### Shortcuts
`Tab` - auto complete

`Ctrl+C` - hard stop

`Ctrl+Z` - jump back to shell, and `fg` brings back to a running program
`Ctrl+D` - exit the current shell, same as `exit` 
`Ctrl+L` - clear screen, same as `clear`
`Ctrl+A` - jump to the beginning of the line
`Ctrl+E` - jump to back of the line
`Ctrl+K` - remove all commands behind the cursor
`Ctrl+U` - remove all commands before the cursor
`Ctrl+W` - remove commands before the cursor upto a space (beginning of the word)
`Ctrl+Y` - paste what has been deleted.
`Ctrl+P` - view previous command, same as `up arrow`
`Ctrl+N` - view the next command, same as `down arrow`
`Ctrl+R` - find old commands that matches your keyword. Press `Esc` to cancel or `enter` to execute.

Use `cmd + d` for vertical split and `cmd + shift + d` for horizontal split

### File Management
Count number of files: `ls | wc -l`

Locate a file in subdirectories: `find <dir1> <dir2> -name "<filename>"`

`ps` shows information of running process
`awk` filter text
`sed` remove part of the text

## ROOT



### Interactive Commands
Make 1d histogram
```
vertex_tree->Draw("sqrt(2.0*reco_shower_energy_max[i_shr[0]]*reco_shower_energy_max[(i_shr[1])]*(1.0-(reco_shower_dirx[0]*reco_shower_dirx[1] + reco_shower_diry[0]*reco_shower_diry[1] + reco_shower_dirz[0]*reco_shower_dirz[1])))/1000>>h(60,0,1.5)","reco_asso_showers==2&&reco_asso_tracks==0")
h->GetXaxis()->SetTitle("Invariant Mass of 2 showers [GeV]")
```

Make 2d histogram `(y:x>>(ybin,xbin))`
```
vertex_tree->Draw("reco_asso_tracks:reco_asso_showers>>g(10,0,10,10,0,10)","1","COLZ")
g->GetYaxis()->SetTitle("Reco Track Number")
g->GetXaxis()->SetTitle("Reco Shower Number")
```
Save Scan log for a TTree named `vertex_tree`:
```
vertex_tree->SetScanField(0);
.> output.txt
vertex_tree->Scan("run_number:subrun_number");
.>
```

**use `sort u` in VIM to remove duplicated rows**

### Common functions
[STDMath](https://en.cppreference.com/w/cpp/numeric/math)

Get maximum @ root:
```
ROOT::Math::Maximum(1,2)
TMath::Max(2,3)
max(2,3) //FROM STDMath, ONLY THIS WORK WITHIN ARGUMENTS
```


[Special Functions](https://root.cern.ch/doc/master/classTTree.html),e.g.
`Max$` will return the maximum value of the expression when iterating over the element of the collection(s) for a given entry.


#### Vectors
In the case of # of showers/tracks:
|Variable|#shower>0 #track>0|#shower==0 #track>0 |#shower>0 #track==0|
|---|---|---|---|
|reco_show| non-null | null | non-null|
|reco_track| non-null | non-null | null|
|f(reco_show,reco_track)| non-null | null | null|

null means it contribute no entries to the histogram; but it could return value `0` (this `0` is actually null, nullify the calculation) in the `Scan` function.

## VNC remote screen
Follow the set up [script](https://sbnsoftware.github.io/sbndcode_wiki/Viewing_events_remotely_with_VNC.html).

To run it, 
1. open a terminal and run `~/openvnc.sh`, success message: 
```
vncserver :45 not running.  Starting now....


New 'uboonegpvm01.fnal.gov:45 (klin)' desktop is uboonegpvm01.fnal.gov:45

Starting applications specified in /nashome/k/klin/.vnc/xstartup
Log file is /nashome/k/klin/.vnc/uboonegpvm01.fnal.gov:45.log
```
2. go to [vnc://localhost:5901](vnc://localhost:5901) in a local browser, use passwd:`123qwe`

3. Use it; for example, a `TBrowser`: open a root file then use command `Tbrowser <any_name>`

## BASH
`env` shows all environment varaibles, i.e. those set by export

`chmod ugo+x <bash_script.sh>` makes the script clickable
### Alias
```bash
VAR=1
VARNAME="VAR"
```

`$VARNAME` access `VAR` as a string.

`${!VARNAME}` access the value of the `VARNAME`, which is `1` in this case.



## Anything Wiki
### Do you know about colors?
[Color Code](http://www.javascripter.net/faq/rgbtohex.htm)
[Color Name](https://www.color-name.com/hex/)
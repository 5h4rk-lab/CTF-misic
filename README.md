# Writeups of CTF made by _5h4rk_

## TASK-1 
Disc:- all you need is good observation power my friend. <br>
file:- observation.txt
Solution:- 
```
when you observe the text file clearly you will notice that joining first letter of every 
line gives you a link of https://pastebin.com and at the end you will find there is a odd line 
which says "aha! this looks helpfull:- wtEQsyUy" that last part completes the incomplete link
so the total link is https://pastebin.com/wtEQsyUy. when you navigate to this you will find the flag
flag:- cyb3rg4abs{p4sT3_Bin_Is_interesting_isn't_It??}
```

## Task2
Disc:- bunch of zips with mpin! <br>
file:- last1.zip <br>
Solution:- 
STEP1:-
=> This has two methodes to solve.
Methode 1
-> script it as discription mentioned says it as mpin which means <Br>
every file is encrypted with 6 digit pin and move on..
#script:-
```
#!/bin/bash
# creating numerical list
echo "[-]creating a word list list"
crunch 1 6 1234567890 -o num.list &>/dev/null
echo "[-]running fcrackzip as long if needed"
while [[ true ]];do
	file=$(ls | grep zip)
	fcrackzip -u -D -p num.list $file > result
	pwd=$(cat result | tr -d '\n' | awk '{print $5}')
	result=$(cat result | tr -d '\n' | grep FOUND)
	if [[-z $result ]]; then
		echo "no pass found in $file"
		break 2
	else
		echo "pass found"
		unzip -q -P "$pwd" "$file"
		rm $file
	fi
done
```
methode 2:- 
 do every thing manually xD;
 
After unziping all the files you will get a hex file <br>
convert it to text and then into image. flag is yours :)
![flag](https://github.com/5h4rk-lab/CTF-misic/blob/master/image1.png)


# CRYPTO
## Task name "Based" 
Disc:- Bases can do many more things. <b>
 file name baseisfun.txt

Solution:-
=> from the name it self we can get to know it is a base encrypted text. <br>
as description says base can do many more things that means it can also hide files <br>
so using this [base to text](https://base64.guru/converter/decode/file) we can convert <br>
based text to a file then you will get a zip just brute force it with rockyou.txt <br>
and the flag is yours. <br>

```
flag:- cyb3rg4abs{Ev3ry_B4s364_is_not_3ncrypt3d}
```

hope you enjoyed the challenges :) .
























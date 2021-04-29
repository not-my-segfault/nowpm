# nowpm

the no-bullshit wpm utility

you know the gist by now. you want to know how fast you can really type, but you're either on a slow connection, don't have a timer and calculator on hand, or think that all those typing speed websites are just tacky.

we've all been there

we all know how it feels



introduring `nowpm`, the wpm utility that just *does it's job*.

![](screenshot.png)



all you have to do is run `nowpm /path/to/file x`

x being the amount of words you want to grab from the file

the words are taken at random, and all lowercased (we're testing typing speed, not how fast and how often you can edge over to shift)

# install instructions

- clone the repo to your system

  `git clone https://github.com/jnats/nowpm`

- make sure install.sh is set as executable

  `chmod +x install.sh`

- run install.sh

  `./install.sh`



# dependencies

nothing big for this one, most of these you should find on any unix-based/like os.

make sure you have these: 

- either does or sudo (for install.sh (or just run `install.sh` as root))

- bash
- wdiff
- sed
- sort
- head
- tr
- python
- bc
- cp
- a readable and writable /tmp

#### addendum 1 : wpm

wpm is calculated by taking your cps (characters per second) and dividing it by the average amount of characters in a word.



the amount of characters in a word is calculated by taking the average of two values

- the average length of a "function" word (3.13)

- the average lenth of a "content" word (6.47)

  

this means the wpm is calculated based purely on averages, and as such may not be 100% accurate

both of these values were taken from page 382 of [this](https://pdf.sciencedirectassets.com/273276/1-s2.0-S0019995800X01489/1-s2.0-S0019995858902298/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEAAaCXVzLWVhc3QtMSJGMEQCIC0AQouiHxgNG1A1zSyDqbh6vAPSlJKDE5U8m6%2F2zUtVAiAIixi1423eDwzFXULg5wvGqrf1yj%2FtZaKYETUF%2FzU3yiq0Awh4EAMaDDA1OTAwMzU0Njg2NSIMqcwvq5n2WkW5GangKpEDuJpMCfuZ7e5o4dSSS8VOjGB605qzJTW6uhiEdDjrbwuRedQ%2FsFoVeE2dtQY6KKdSLRjSRbzW4IU3NAWRgmRnCHX6D2xdYpXahB0Hhw6m5XHuOC4f4q99mp%2FjvJXQPU7vLNMeCYGu2%2BUjddlqHS0b4Wo9InZF%2FQmr%2FLXbEAD3mmXN3dzR1y2gkjzEVYCryGuIlex%2F5%2FXPGRFQveSj7q0ZudmeoAWfm275aN%2BMwL4kna3Kx%2BAu8jNEa0Y1t7Jo%2FE6bOVtX1RPouQX3%2F8sGgiM3M%2BPfErzEAJktMqrYqWnNottGgGkg47LQaFc5Rdhy%2F7bArdbydKTg%2B%2BF5nIHBEodwQ0ejmuZo12kKje3qlcI%2BvfS%2BJxkd3%2F3UVngKfP0UZKjRRjlgwWBqWAmDfOMqRR%2FPRMWrQdBcIKULSEx5eh07wn5FaeGjVHUWI6qarsFd5ASEAl4wCvyLtCT9tMom7bRhQZhNs%2BJWswAvrE%2FZIxDM73fJvOpFIorUnbm3bErHD1KdRdos3v1N811f%2FOwbnWY6cBAwn5arhAY67AFGK%2ByWf3I7op5JKsnOBunzYsO1%2Fl3evA0Yo5hqmzImq9RUSgNTtVBvvVPobtRYXIRB6AUNxzaTXQ0cTgW%2Bav%2BenkruEcxmUfN3K9j3XLGf8lNhbuj8hnnopr50NtDSuAq2NOx4KR4A0XbZOOu2Ewb%2F%2B2Wdn0rsh%2FI8SSs6UM5PlP3IL6XFCAIwUL0iA7H%2B5uDNuqgqQjntoFDp982VHpkRtamyl0LhRQ1oFIPX7fMx9SswZtOZXsrdWUdMa12mJevrMvoTF8E93EcqocOyCbhirMSfSzHpH7d8fQBvSQzM6PkNRO6yXA4RwREe%2Bg%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20210429T165101Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYSA3UHZ3E%2F20210429%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=5ed3e3c845fe32e8acfa2cebe746447b7a9fa3945595e9568b3bf5b3ab624ebb&hash=642cd11983e194c627f75200365bd24c90d9de7e6547e3f8e8a43aef5dea7c65&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S0019995858902298&tid=spdf-544fde50-f4a3-4fa8-b824-6625b5dff3b0&sid=6073e9d623368443666a09994cd0cd361367gxrqb&type=client) scientific paper

#### addendum 2 : time taken

the time taken is calculated by

- parsing a miniature pythons script to grab the current time in ms *right as* the typing prompt appears
- parsing said script again after you hit return/enter
- calculating the difference between these
- dividing by 1000 to get the time in seconds



i chose to call python instead of ` date -u %N` for one simple reason



*i do not primarily use linux.*



the %N feature is *not* available on *BSD systems *or* macOS (which also uses FreeBSD coreutils)

and since i write these programs to be able to work for *anyone*, i have made the active choice to run the python code instead. in my belief, it is reasonable to have python installed, but you shouldnt have to replace your own coreutils with GNU ones just to check the milliseconds, especially since more people now than ever are trying alternative options.
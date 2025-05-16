# 🧬 Bash One-Liner Survival Kit for Bioinformaticians
**_When your coffee is cold and you want results in a few minutes without losing your sanity._**  

> **Welcome folks!**<br> 
> This kit may save you and your sanity. Below are some bash one-liners to save your day as it did mine.

***
## 🔪 Count how many sequences are in that 10GB FASTA
```
grep -c "^>" file.fasta
```
📌 When someone says, "I downloaded this genome. How many sequences are in it?" Just run this and find out. 

***
## 🔎 Grab only the headers from a FASTA
```
grep "^>" file.fasta | sed 's/^>//'
```
📌 You need just the sequence IDs to compare against an Excel sheet someone sent you.

***
## 🔂 De-duplicate that mysterious gene list someone copy-pasted from six Excel tabs
```
sort file.txt | uniq
```
📌 The collaborator assures you the gene list is “totally non-redundant” except when it’s not.

***
## 🎯 How many reads actually mapped? (Be honest.)
```
samtools view -c -F 4 file.bam
```
📌 You were blaming the low expression on biology, but turns out nothing mapped in the first place.

***
## 🏆 Find the longest contig, because size matters (in assemblies)
```
awk '/^>/ {if (seqlen){print seqlen}; seqlen=0; next} {seqlen+=length($0)} END {print seqlen}' file.fasta | sort -nr | head -1
```
📌 You need a table of top contig lengths in few seconds.

***
## 📂 Split a multi-FASTA into individual files because some tool will ONLY insist on it.
```
awk '/^>/{f="seq"++i".fa"} {print > f}' file.fasta
```
📌 A tool you found does your work but only accepts single-FASTA input, then split it up and wait for impact.

***
## 🧪 Quick sanity check: is this FASTQ file huge or stupid?
```
du -h file.fastq; wc -l file.fastq
```
📌 Wondering why your disk quota disappeared overnight?

***
## ☠️ BLAST job ran off the rails? Kill it with fire.
```
ps aux | grep 'blastn' | awk '{print $2}' | xargs kill -9
```
📌 That blastn you launched 3 days ago is now consuming 95% of the server's memory.

***
## 📊 Get read counts from all your FASTQ files in one  swoop
```
for f in *.fastq; do echo -n "$f "; echo $(($(wc -l < "$f")/4)); done
```
📌 When the text says “Hey can you send me read counts for all the samples, like now?” Bash it out before they finish typing "Thanks"

***

> Work in progress—just like my code, my pipeline and my life. This list will grow as I continue breaking things and figuring out how to fix them. If you have got hacks of your own, feel free to add, future us will thank you 😊.

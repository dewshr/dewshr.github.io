---
title: Linux Tips
author: Dewan Shrestha
date: 2022-08-22 13:30:00 -0500 
categories: [linux]
tags: [awk, sed, shell, condition, tar]
pin: true
---

**Create a directory with multiple sub-directories**

`mkdir -p output_folder/{raw_data,temp_data,result,log_folder}`

**Compress and decompress file**

compress: `tar -zcvf compressed.tar.gz *.csv`

extract: `tar -xzvf compressed.tar.gz`

**Change the value of specific column given a condition (if else)**

`awk '{print $1,($2<0)? 0 : $2,$3}`

**Find common lines between two files**

`comm -12 >(sort file1) <(sort file2)`

**Replace empty columnn with certain value**

`awk -F, 'BEGIN {FS=OFS}{if ($7=="") $7="changed"; else $7=$7; print}' input_file.txt > modified_input.txt`

Here, 7th column is replaced by value `changed` if its empty else, original value is kept

**Getting all the rows with 2 columns having same values**

`awk '($4==$5)' input_file.txt > output_file.txt`

**Filtering rows based on certain column value**

`awk '($4 < 5)' input_file.txt > output_file.txt`

**Filering using multiple conditions**

`awk '($4 <5 && $4 >0)' input_file.txt > output_file.txt`

**Getting mean value for specific column**

`awk {total +=$4} END {print total/NR} input_file.txt`

**Getting unique values based on multiple column comparison**

`awk -F"\t" 'seen[$1,$2,$3,$4]++' input_file,txt > output_file.txt`

**Removing first row without opening file**

`sed '1d' input_file.txt > output_file.txt`

**Changing the values of file**

`sed 's/-/\t/g' input_file.txt > output_file.txt`

**Sometimes there are carriage returns (\r, ^M) in file, which can mess up the file processing, you can remove it by:**

`sed 's/\r//g' input_file.txt > output_file.txt`



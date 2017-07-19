---
layout: post
title:  "Using bash for git clone automation"
permalink: bash-automation
---

Recently I wanted to automate most of my professional obligations. As a university lecturer, I have to deal with tons of assignments. Grading and managing those stuff is tedious.

One of my teaching areas is computer programming. And I love giving projects to finish as the final assessment. This year I decided to try something new. I asked the students to upload their project to Github. I then cloned their projects to my local machine at the previously-agreed deadline time. And my goal is: to automate this.

This sounds way too novice, but as someone who has never seriously explored bash scripts, it is a nice mini challenge. I've used bash scripts before, however it's merely for something simple, like makefile. So, I started by designing the automated workflow.

### Recording the Github ID

I had asked the students to create Github accounts in the beginning of the semester. Github has become a standard for portfolio showcase in the programming world. Thus having one is a necessity for newcomers, including the students.

I recorded their names and Github IDs in a CSV file. The format is the name of the student and then followed by the Github ID separated by a comma. The following is an example of the CSV file.

```csv
Student one,studentOneGithubID
Student two,studentTwoGithubID
```

After completing the database, I proceeded to the next step. Writing the bash script.

### Bash Script

Bash is a completely different world. Coming from C-family programming languages, bash, for me, is like an animal from another universe. However, I found it engaging to conquer a distinct beast.

The flow of the bash script is the following:

1. Read line-by-line the previous CSV file.
2. Split the line using comma as the delimiter and store the values in an array.
3. Create one folder for each student and use the students' names as the name of the folders.
4. In their respective folders, execute `git clone` command to clone the Github repos.
5. If the Github repo of a student is not found, append the name in a variable that contains the list of the students with no git repos.

```bash
#!/bin/bash

filename="$1"
gitrepo="final-web2-unai-2017"
unsuccessfulclone=0
unsuccesslist=""
while read -r line
do
	IFS=',' read -r -a array <<< "$line"
	echo "Creating folder ${array[0]}"
	mkdir "${array[0]}"
	echo "Entering folder ${array[0]}"
	cd "${array[0]}"
	repo="https://github.com/$(echo -e "${array[1]}" | tr -d '[:space:]')/$gitrepo.git"
	echo "    Cloning github $repo..."
	GIT_TERMINAL_PROMPT=0 git clone "$repo" || { unsuccesslist+="${array[0]}\n"; ((unsuccessfulclone++)); }
	echo "    DONE"
	cd ..
done < "$filename"
echo "DONE"
echo "Unsuccessful clone: $unsuccessfulclone"
echo -e "${unsuccesslist}"
```

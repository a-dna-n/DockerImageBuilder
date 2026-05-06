## Introduction

I wrote almost all of the code in this repo, like 99% of it. It was a complete rewrite of a complex collection of scripts and config files that was context-dependent, difficult to use, very difficult to update, and basically Bash-based. This rewrite and many of the implementation details were my ideas. It is a partial first step from Bash to Python because it met multiple needs.

More to come.

## Previous implementation of Docker Image Builder

Briefly, the code in this repo replaced a collection of ~125 scripts and config files, including 75 Bash scripts, partly organized here but originally in a single folder:

<img width="1749" height="388" alt="image" src="https://github.com/user-attachments/assets/59572c26-84c5-42bb-8bcc-d346886b139c" />

<br><br>
Dockerfile contents looked like this, intentionally illegible:

<img width="1912" height="1008" alt="image" src="https://github.com/user-attachments/assets/1e8df6e8-b81e-4aa4-85db-8dc1f06e6ebe" />

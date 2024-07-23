# [oBfsC4t10n2](https://app.hackthebox.com/challenges/120)

> Author: Nayanjyoti Kumar

## DESCRIPTION:
Another Phishing document. Dig in and see if you can find what it executes.

## STEPS:
1. Unzipping the .zip file shall resulting to an excel file.
![241874508-664282f4-9f76-457d-abed-9c576f785a94](https://github.com/user-attachments/assets/0afd53b8-c04d-4b5d-9781-aae8dce09c8c)

2. Since it's an excel file, let's check are there any VBA Macros.
3. To check that, run **olevba** to it.

> RESULT

![241874745-7f19d696-e9ee-41d4-ab60-3d64f001b258](https://github.com/user-attachments/assets/48cb6540-a586-42a7-87af-59e82f0a70bd)

4. Actually we got very long result.
5. Analyzing the result we're noticing several flags partition look alike.

> KEEP SCROLLING DOWN, HENCE U'LL FIND SIMILIAR PATTERN.

![Screenshot 2023-05-30 140636](https://github.com/Bread-Yolk/hackthebox/assets/70703371/316149a9-ae7f-456c-9b2b-0fb5e1b380ac)


![Screenshot 2023-05-30 141013](https://github.com/Bread-Yolk/hackthebox/assets/70703371/e25a258d-153b-4cf1-a623-455c3016d8f3)


![Screenshot 2023-05-30 141248](https://github.com/Bread-Yolk/hackthebox/assets/70703371/c15a8d67-2766-4136-91a3-1b4fd30896c7)


6. This writeup must be not intended, because i didn't analyze the script pattern, i just searched for every strings that look alike CTF flag.
7. For the partition order, obviously i started with the HTB{ prefix, then continue with Xc3l.
8. The final part is 4.0_.
9. Got the flag!

## FLAG

```
HTB{n0w_eXc3l_4.0_M4cr0s_r_b4cK}
```



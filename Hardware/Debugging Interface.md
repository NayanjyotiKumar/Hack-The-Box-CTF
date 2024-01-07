# [Debugging Interface] (https://app.hackthebox.com/challenges/debugging-interface)
> Author: Nayanjyoti Kumar

## DESCRIPTION:
We accessed the embedded device's asynchronous serial debugging interface while it was operational and captured some messages that were being transmitted over it. 
Can you decode them?

## STEPS:
1. First, unzip the `.zip` file given.

2. Check the file type.

3. Since the file's extension is `.sal`. Means we have to download the saleae logic analyzer from google and analyze using it.

4. Now open the file in saleae logic analyzer.

5. After unzipping the file, there are two additional files it, named as: digital-0.bin and meta.json.

6. Now, some information about these files:

> RESULT

![image](https://github.com/ValhalaKing16/Hack-The-Box-CTF/assets/94128525/04adca7c-49c0-403c-aac4-f443e7a8d7e9)

Used the ‘strings’ command to extract human-readable text strings from binary files (digital-0.bin), and saw that the first line was ‘SALEAE.’

7. Now choose the `analyzer` tab then click the `Async Serial`.

> RESULT

![image](https://user-images.githubusercontent.com/70703371/208970027-69f2bed7-ef1d-4f2d-960a-9d9e91d503e1.png)

![image](https://user-images.githubusercontent.com/70703371/208970324-665f33b4-12c4-4acb-b33b-8dbc300d7b5b.png)


8. Click save.
9. We can see that there are many framing errors.

![image](https://user-images.githubusercontent.com/70703371/208970545-641c445d-e5bd-4b7c-a9e3-ea38bd97c3ee.png)

![image](https://user-images.githubusercontent.com/70703371/208970938-dee35f55-5af6-4dbc-b6cb-2542c82ef05e.png)


10. Change the data representation to ASCII.

> RESULT

![image](https://user-images.githubusercontent.com/70703371/208971058-9cab0bc8-f740-40c3-aa63-36eb58248939.png)


11. Now let's solve the framing errors.
12. A framing errors occurs when the bit being read is too fast or too slow.
13. If the bits are being read too fast or too slow, the bits will give different values.
14. To fix the errors simply find the each shortest interval.
15. Based from the graph we know that the shortest from each is 32.02 microseconds.
16. Hence to calculate the actual bit rate, we shall use this formula:

```
Actual Bit Rate = 1 / (32.02 * 10^(-6)) -> 31230.480949406621
```

17. Since there's no decimal place in number of bits to read, so we can exclude the decimal number.
18. At the `Async Serial` click edit.
19. Change the bit rate value.

![image](https://user-images.githubusercontent.com/70703371/208973575-74a6ba75-a490-4249-9e62-8253bc12bc5f.png


20. Now click save.

> RESULT

![image](https://user-images.githubusercontent.com/70703371/208973645-bc3c5a6b-fa0b-4e4d-aeb0-8c1020a7b5e2.png)


21. Change the data results to terminal.


![image](https://user-images.githubusercontent.com/70703371/208973785-c4f9145c-a617-4191-96d3-a7ceb18f81f4.png)


![image](https://user-images.githubusercontent.com/70703371/208973848-c083ca5d-72c6-40b0-805a-eb875881b00f.png)


22. Got the flag!


## FLAG

```
HTB{d38u991n9_1n732f4c35_c4n_83_f0und_1n_41m057_3v32y_3m83dd3d_d3v1c3!!52}
```

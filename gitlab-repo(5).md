# A Noob's First Milestone - CTF Writeup

**Category:** OSINT  
**Points:** 150 pts  

---

## 🧩 Challenge Description

> His first gitlab repo.

The challenge description was minimal but clear — we needed to find someone's first GitLab repository. The key was identifying who "he" refers to.

```
Creator - pandasif
```

This gave us our first lead: **pandasif** was likely the person whose GitLab repo we needed to find.

The challenge title "A Noob's first milestone" suggested we needed to look at their **very first repository** — possibly their earliest commit or first project on GitLab.

---

## 🧠 Approach

### Step 1: Locate the GitLab Profile

We searched for the user **pandasif** on GitLab:
```
https://gitlab.com/pandasif
```

### Step 2: Identify the First Repository

Once on their profile, we looked for:
- Their oldest/first public repository
- Repository creation dates
- Commit history in early projects

### Step 3: Analyze the Source Code

We found a repository containing a C++ source file (`sk.cpp`) that simulated a "script kiddie" attack tool. This matched perfectly with the challenge theme "A Noob's first milestone."

### Step 4: Examine the Code Carefully

Looking through `sk.cpp`, we noticed three data arrays used to generate random email addresses:
```cpp
const vector<string> FIRST_NAMES = {
    "olivia","emma","amelia","ava","sophia","charlotte","isabella","mia","luna","harper",
    "liam","noah","oliver","elijah","lucas","levi","mason","asher","james","ethan",
    "EOF"  // ← Hidden here!
};

const vector<string> SURNAMES = {
    "smith","johnson","williams","brown","jones","garcia","miller","davis","rodriguez",
    "martinez","hernandez","lopez","gonzales","wilson","anderson","thomas","taylor",
    "moore","jackson","martin","{script_kiddie"  // ← Hidden here!
};

const vector<string> EMAIL_PROVIDERS = {
    "gmail.com","outlook.com","yahoo.com","aol.com","yandex.com","eofool.com}"  // ← Hidden here!
};
```

---

## 💡 Discovery

The flag was cleverly hidden across three arrays:

1. **FIRST_NAMES** array - last element: `"EOF"`
2. **SURNAMES** array - last element: `"{script_kiddie"`
3. **EMAIL_PROVIDERS** array - last element: `"eofool.com}"`

When pieced together, these elements form the flag: **`EOF{script_kiddie}`**

The creator hid the flag in plain sight within the data structures used by the script kiddie simulation tool — a fitting easter egg for a challenge about a "noob's first milestone"!

---

## 📸 Evidence

The flag components were embedded in the source code arrays:
```cpp
// Flag parts hidden in plain sight:
"EOF"                  // From FIRST_NAMES
"{script_kiddie"       // From SURNAMES  
"eofool.com}"          // From EMAIL_PROVIDERS
```

---

## 🏁 Flag
```
EOF{script_kiddie@eofool.com}
```

---

## 🧾 Summary

| Step | Action                                    | Result                              |
| ---- | ----------------------------------------- | ----------------------------------- |
| 1    | Identified creator from previous challenge| Found username: **pandasif**        |
| 2    | Searched GitLab for user profile          | Located profile at gitlab.com/pandasif |
| 3    | Found first/early repository              | Discovered `sk.cpp` source code     |
| 4    | Analyzed source code arrays               | Found flag split across 3 arrays    |
| 5    | Reconstructed flag components             | Success!                            |

---

---

## 🛠️ Tools Used

- **GitLab Search** - To locate the user profile
- **Browser** - To navigate repositories and view source code
- **Text Editor** - To analyze the C++ source file

---

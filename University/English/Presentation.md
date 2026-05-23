#### SLIDE 1 — Title

_[Speak calmly, make eye contact, no rush]_

"Hi everyone. My name is Roman Khimin, and today I want to talk about something that most researchers completely overlook — until it's too late."

---

#### SLIDE 2 — Hook

_[Pause after each question. Look at the audience, not the screen.]_

"Imagine this. You find a dataset online. It looks perfect for your research. You download it, open it up — and then you see columns named things like... _'col_x_v2_FINAL'._

_[Small pause — let the audience feel it]_

What does that mean? What software created this file? What do the missing values represent? Was this data even collected correctly?

_[Slightly faster, then slow down for the punchline]_

You spend hours trying to figure it out. You email the author. No reply. The paper it came from is behind a paywall. The research is essentially... lost.

_[Pause]_

One simple text file could have prevented all of this. It's called a README."

---

#### SLIDE 3 — What is a README?

_[Relaxed, like explaining to a friend]_

"So what exactly is a README? It's a plain-text file that travels with your dataset and answers the most basic questions: _what_ is this data, _how_ was it collected, and _how_ do I use it.

Think of it as the instruction manual that comes with IKEA furniture — except for your data. Without it, even a perfectly collected dataset becomes useless to anyone else.

And honestly? Useless to future you as well. Six months from now, you won't remember what _'col_x_v2_FINAL'_ meant either."

---

#### SLIDE 4 — Core Elements

_[Confident and clear — name each element, don't read the descriptions word for word]_

"A good README has five core elements.

First — **title and creator**: who made this, when, and how to contact them.

Second — **methods**: how the data was actually collected. What instruments were used, what was the sampling strategy.

Third — **variables**: every single column, defined. Name, unit, what values are allowed, and what the missing data codes mean.

Fourth — **file formats**: what type of files are included, and what software opens them.

And fifth — **license**: who is allowed to use this data, and how.

That's it. Five things. But without them, your dataset is a black box."

---

#### SLIDE 5 — Folder Structure & File Naming

_[A little humor here works well]_

"Now, a README doesn't exist alone. It lives inside a well-organized folder.

_[Point to the folder tree on the slide]_

Here's a simple example: raw data in one folder, processed data in another, scripts in a third. And right at the top — the README.

And please — _[slight smile]_ — look at these file names. _'data FINAL v2 USE THIS dot xlsx'_. We've all seen something like this. We've all probably made something like this.

Compare that to _'2024-03-15_survey_clean.csv'_ — instantly you know what it is, when it was created, and what stage it's at.

The rule is simple: use the date first, no spaces, lowercase, be descriptive. Your future collaborators — and your future self — will be grateful."

---

#### SLIDE 6 — Software & Dependencies

_[This is the 'surprising fact' moment — deliver it with weight]_

"Here's something people often forget.

_[Pause]_

Code that runs perfectly today may fail completely in two years — just because a library updated.

That's why your README must document the software environment: the programming language and its version, the libraries you used, and the operating system. Even something as simple as _'Python 3.11.2, pandas 2.0.1, install with pip install -r requirements.txt'_ can save someone hours of debugging.

This is especially important in machine learning and data science, where environments change fast."

---

#### SLIDE 7 — Across Disciplines

_[Energetic, show it's universal]_

"Now you might be thinking — okay, this sounds like a CS thing. But READMEs are used across every field.

In biology, you document the species sampled, the instruments used, what 'NA' in your data actually means.

In economics, you explain the time range, the data source, whether values are in 2015 constant dollars.

In machine learning, you describe the dataset split, the preprocessing steps, the exact framework version.

The structure adapts to the field — but the goal is always the same: make your data understandable for anyone, anywhere, at any time."

---

#### SLIDE 8 — README vs Metadata

_[Slightly more academic tone, but still clear]_

"There's one more concept worth understanding: the difference between a README and metadata.

A README is written for _humans_ — it's informal, narrative, stored right next to your data files, created by you, the researcher.

Metadata is written for _machines_ — it follows standardized schemas like Dublin Core or DataCite, lives in a repository catalog, and is often generated automatically.

They're not competing — they complement each other. A README informs humans. Metadata informs machines. Together, they make your research truly FAIR: Findable, Accessible, Interoperable, and Reusable."

---

#### SLIDE 9 — Conclusion

_[Slow down, make it land]_

"So let's recap.

A README is your data's instruction manual. Five core elements: title, methods, variables, formats, license. Good folder structure and file naming make everything reproducible. Always document your software versions. And together with metadata, a README makes your research genuinely open.

_[Pause — look at the audience]_

The next time you finish collecting data, before you share it, before you upload it, before you move on to the next project —

_[Slight pause for effect]_

Will you write the README first?"

---

**A few delivery tips:**

- The hook on slide 2 only works if you pause — don't rush through the questions
- On slide 5, the bad filename example is a natural moment for a brief smile — use it
- The closing question is your ending — after you say it, just stop. No filler, no "that's all", no "thank you for your attention"
- Total words: ~620 — at a comfortable speaking pace that's right around 3:30
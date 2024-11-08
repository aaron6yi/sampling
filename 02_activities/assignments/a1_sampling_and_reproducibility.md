# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: YI ZHANG


#### Q1 :
The blog post by Andrew Whitby dives into how contact tracing can give a skewed view of where infections are happening. The code for this model mimics that scenario by simulating infections at two types of events—weddings and brunches—and then seeing how contact tracing changes what we think about where infections started.

Step 1: Setting Up Events and Attendees
In the model, there are 1,000 people, split into two groups: 200 go to weddings and 800 to brunches. This split sets up our scene, showing that some events are bigger than others, which mirrors real life. These people become our “sampling frame,” or the pool we’re drawing from.

Step 2: Infecting a Random Subset
The first sampling happens when the model infects 10% of these attendees. This means around 100 people randomly get infected, and it’s done without replacement (so no double infections). Each person, whether they’re at a wedding or brunch, has the same chance of infection. So, the infection here is pretty straightforward and evenly spread.

Step 3: Primary Contact Tracing
Next up, the model performs primary contact tracing on the infected group. This is where it gets interesting: each infected person has a 20% chance of being traced. So, if someone is infected, there’s a 1-in-5 shot they’ll get tagged as “traced.” This sampling step is like flipping a coin with weighted odds for each infected person. It only applies to those already infected, so it’s conditional sampling.

Step 4: Secondary Contact Tracing (Adding a Bias)
Now, here’s where the bias starts to sneak in. If any event has at least two traced infections, everyone infected at that event is also traced, no matter what. It’s not random this time—it’s a rule. So if a wedding hits that threshold, all infected wedding attendees automatically get traced. This creates a kind of feedback loop where bigger or more “traceable” events (like weddings) start to look like hot spots, even if brunches have just as many infections.

#### Q2:




## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.

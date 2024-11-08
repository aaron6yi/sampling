# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: YI ZHANG

#### Q1

**Stage 1: Setting Up Events and Attendees**

- **Procedure**: The model creates a simulated population of 1,000 individuals, assigning them to two types of events: 200 people attend weddings, and 800 people attend brunches. This setup mimics real-world scenarios where certain event types naturally attract larger groups, as brunches do here.
- **Function Used**: Assignment is based on predefined proportions for each event type, manually dividing individuals into either wedding or brunch attendees.
- **Sample Size**: Total population of 1,000 individuals, divided into two event types (200 for weddings, 800 for brunches).
- **Sampling Frame**: The entire population attending events (1,000 people), which represents the pool from which we draw samples for infection and tracing in later stages.
- **Underlying Distribution**: Not randomly assigned, but fixed according to proportions that reflect different event attendance sizes—ensuring that some events are larger and more populated, setting up realistic conditions for infection and tracing.


**Stage 2: Infecting a Random Subset**

- **Procedure**: The model randomly infects approximately 10% of attendees (controlled by `ATTACK_RATE = 0.10`), simulating a random infection process across the total population.
- **Function Used**: `np.random.choice` is used to randomly select individuals from the population without replacement, ensuring each infected person is unique and no "double infections" occur.
- **Sample Size**: Determined by `int(len(ppl) * ATTACK_RATE)`, which results in around 100 infected individuals.
- **Sampling Frame**: The entire population of event attendees (1,000 people) from which infected individuals are randomly selected.
- **Underlying Distribution**: Uniform random sampling, giving each attendee an equal chance of infection. This represents an unbiased infection spread and simulates a scenario where exposure could happen anywhere within the attendee population.


**Stage 3: Primary Contact Tracing**

- **Procedure**: In this stage, the model applies primary contact tracing to the subset of infected individuals. Each infected person has a 20% probability of being traced, simulating a process where contact tracing may not cover all infected cases.
- **Function Used**: `np.random.rand`, combined with a comparison operation (`< TRACE_SUCCESS`), is used to assign a 20% tracing probability to each infected individual, mimicking real-world tracing variability.
- **Sample Size**: Dynamic, depending on the number of infected individuals (initially around 100 based on the infection rate).
- **Sampling Frame**: Infected individuals only, making this a targeted sampling approach that applies solely to those who were already infected.
- **Underlying Distribution**: Bernoulli trial with a probability of 0.20, where each infected person has a 20% chance of being flagged as traced. This probabilistic approach captures real-world limitations in contact tracing, where not every case is traced.

**Stage 4: Secondary Contact Tracing (Introducing Bias)**

- **Procedure**: Secondary tracing introduces bias by marking all infected individuals at an event as traced if that event reaches a threshold of two or more traced cases. This rule-based approach causes certain events, especially larger ones like weddings, to appear as infection hotspots, even if brunches have similar infection rates.
- **Function Used**: `ppl.loc[ppl['event'].isin(events_traced) & ppl['infected'], 'traced'] = True`, which traces all infected attendees at events that meet the tracing threshold.
- **Sample Size**: Variable, depending on the number of events that reach the threshold of two traced cases.
- **Sampling Frame**: Events with two or more traced infections, which amplifies visibility at certain events and introduces sampling bias.
- **Underlying Distribution**: Deterministic rule-based sampling rather than a random process. This feedback loop results in an overestimation of risk at certain events, aligning with the blog post's explanation of how contact tracing visibility can distort perceptions of infection hotspots.

---

#### Q2

Does this code appear to reproduce the graphs from the original blog post?

No, the graph appears different from the one in the original blog post.

---

#### Q3

I reduced the number of repetitions in the simulation from the original 50,000 to 1,000 and ran the script multiple times. Each time, the plot looks slightly different, but the samples generally follow the same distribution.

---
#### Q4

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

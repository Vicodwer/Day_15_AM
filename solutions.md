# Probability & Statistics Assignment Solutions

## Q1 — The Base Rate Fallacy: The Medical Test Paradox

The **Base Rate Fallacy** occurs when people focus on specific information (test accuracy) while ignoring the "base rate" (the actual prevalence of the condition in the population).

### The Example
- **Disease Prevalence (Base Rate):** 1 in 10,000 (0.01%)
- **Test Accuracy:** 99% (Sensitivity = 99%, Specificity = 99%)

### Why are most positives false?
Let's consider a population of 1,000,000 people.

1.  **True Positives:**
    - Since the disease hits 1 in 10,000, out of 1M people, **100 people** actually have the disease.
    - With 99% accuracy, the test will correctly identify **99** of them.
2.  **False Positives:**
    - Out of 1M people, **999,900 people** do NOT have the disease.
    - However, the "99% accurate" test has a 1% error rate for healthy people. 
    - 1% of 999,900 = **9,999 false positives**.

### Conclusion
If you test positive, the pool of "positive results" contains:
- 99 True Positives
- 9,999 False Positives
- **Total Positives = 10,098**

The probability that you actually have the disease given a positive test is:
$$ P(\text{Disease} | +) = \frac{99}{10,098} \approx 0.98\% $$

Even with a "99% accurate" test, you have **less than a 1% chance** of actually being sick. This is because the "noise" (false positives from the huge healthy population) completely overwhelms the "signal" (true positives from the tiny sick population).

---

## Q2 — CLT Simulation (Coding)

The implementation can be found in [clt_simulation.py](file:///C:/Users/Vishal/.gemini/antigravity/scratch/probability_assignment/clt_simulation.py). Below is the core logic:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm
import scipy.stats as stats

def simulate_clt(distribution, params, n_samples, n_simulations):
    # Calculate theoretical stats
    mean, var = distribution.stats(**params, moments='mv')
    std_error = np.sqrt(var / n_samples)
    
    # Generate simulation data
    sample_means = [np.mean(distribution.rvs(**params, size=n_samples)) for _ in range(n_simulations)]
    
    # Plotting
    plt.figure(figsize=(10, 6))
    plt.hist(sample_means, bins=30, density=True, alpha=0.6, color='skyblue', label='Sample Means')
    
    x = np.linspace(min(sample_means), max(sample_means), 100)
    plt.plot(x, norm.pdf(x, mean, std_error), 'r-', lw=2, label='Normal Approximation')
    
    plt.title(f'CLT Simulation (n={n_samples})')
    plt.legend()
    plt.show()
```

---

## Q3 — Exponential Purchase Amounts: The Mean Trap

### Why "Mean Purchase Amount" is Misleading
An exponential distribution is heavily skewed. Most customers spend very small amounts, while a few "whales" spend significantly more. 

- **The Problem with Mean:** Because the distribution has a "long tail," outliers (high spenders) pull the mean significantly higher than what a "typical" customer spends. An investor might see a mean of $100 and think everyone is spending $100, when in reality, 63% of customers spend *less* than the mean in an exponential distribution ($1 - e^{-1} \approx 0.632$).
- **Investment Risk:** If growth relies on a few outliers, the business is less stable than if the "typical" customer spends more.

### What to show instead?
1.  **Median:** The 50th percentile provides a better sense of the "typical" customer experience.
2.  **LTV/CAC Ratio by Cohort:** To show sustainability.
3.  **Percentile Breakdown (P90, P99):** To show how much revenue is concentrated in top spenders.
4.  **Retention Curves:** Frequency matters more than average amount in many business models.

---

## Part D — AI-Augmented Task

### 1. The Prompt
**Prompt:** *"Explain the Central Limit Theorem to a non-statistician product manager. Why does it matter for A/B testing? Include a Python simulation."*

### 2. The Output
> **The "Magic" of the Central Limit Theorem for Product Managers**
>
> Imagine you're trying to figure out the "average height" of everyone in a massive football stadium. You can't measure everyone. So you pick 30 people at random and average them. Then you do that again, and again.
>
> Even if that stadium is full of giants and toddlers (a very "non-normal" distribution), if you plot all your *group averages*, the resulting shape will always be a perfect **Bell Curve**.
>
> **Why this is your A/B Testing Superpower:**
> Most data you track (clicks, spend, time-on-site) is "messy" and doesn't look like a bell curve. It’s often skewed. However, because of the CLT, we know that the *difference* between your Version A and Version B averages will follow a predictable distribution. This allows us to calculate the **p-value**—the probability that the "win" you're seeing is just a fluke of luck.
>
> **Python Simulation:**
> ```python
> import numpy as np
> import matplotlib.pyplot as plt
>
> # Messy data: 90% small spenders, 10% big spenders
> population = np.concatenate([np.random.exponential(5, 9000), np.random.normal(100, 20, 1000)])
>
> # Take 1000 samples of 40 people and plot their averages
> averages = [np.mean(np.random.choice(population, 40)) for _ in range(1000)]
>
> plt.hist(averages, bins=30, color='purple', alpha=0.7)
> plt.title("The 'Bell Curve' of Sample Averages")
> plt.show()
> ```

### 3. Evaluation
- **Accessibility:** High. It uses a stadium analogy and avoids jargon like "homoscedasticity" or "kurtosis." It focuses on the *result* (predictability) rather than the formula.
- **P-value Mention:** Yes. It explicitly connects CLT to p-values, explaining that CLT is the bridge that lets us calculate the probability of "luck" (flukes) in A/B test results.

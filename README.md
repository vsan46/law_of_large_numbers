# **Visualizing the Law of Large Numbers**

I built this little Python script to help visualize one of the most fundamental concepts in statistics: The Law of Large Numbers (LLN).

It's one thing to read the definition in a textbook, but it's another thing entirely to watch it happen in a simulation. This project uses a simple coin-flip analogy to show how reality eventually catches up to theory if you repeat an experiment enough times.

## **What is the Law of Large Numbers?**

In simple terms, the Law of Large Numbers states that as you perform the same experiment a large number of times, the average of the results obtained will get closer and closer to the expected value (the theoretical average).

**The Coin Analogy**: If you flip a fair coin, math tells you there is a 50% chance (0.5 probability) it lands on Heads.

- If I flip it just 10 times, I might get 7 Heads (70%). That's way off the theoretical 50%, but that's just short-term luck (variance).
- The LLN says that if I flip that coin 10,000 times, my final percentage of Heads is going to be incredibly close to 50%.

It doesn't mean the coin "remembers" past flips to balance things out. It just means that over a massive number of trials, the initial noise and luck get drowned out by the statistical average.

## **How My Code Works**

To visualize this, I needed to simulate a ton of coin flips and track the batting average of "Heads" as we went along.

Here is the breakdown of the lln_coin_flip.py script:

### **1. The Setup**

I use numpy for the number crunching and matplotlib for the visualization. I set the total number of trials (N_TRIALS) to 5,000. I also define the goalpost: the theoretical probability of a fair coin is 0.5.

### **2. The Simulation** (NumPy allows me to be lazy here)

Instead of writing a slow for loop that flips a coin 5,000 times one by one, I use NumPy to generate the whole dataset instantly.

outcomes = np.random.randint(0, 2, N_TRIALS)

This line creates a massive array containing 5,000 random integers that are either 0 or 1. We'll treat 1 as "Heads".

### **3. Calculating the "Running Average"**

This is the most important part statistically. I don't just want the final score; I want to see the score evolving.

I use np.cumsum(outcomes) to get a running total of heads.

If the outcomes were [1, 0, 1, 1], the cumulative sum is [1, 1, 2, 3].

I then divide that running total by the trial number (1, 2, 3, 4...). This gives me an array representing the proportion of heads at every single step of the journey.

### **4. The Visualization**

Finally, I throw that data into matplotlib.

The blue line is the experimental data. You'll notice that at the beginning (the left side of the chart), the line is wildly erratic. With only a few flips, the proportion swings massively away from 0.5.

The red dashed line is the theoretical 0.5.

As you move to the right (increasing the number of trials), you can clearly see the blue line settling down and converging tightly around the red line.

That convergence is the Law of Large Numbers in action.

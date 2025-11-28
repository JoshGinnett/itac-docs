# How to Write a Recommendation

Every recommendaiton you write will have the same 5 sections: Summary, Current Practices and Observations, Recommended Action, Anticipated Savings, and Costs and Payback. These sections will never change. You don't need to add or remove sections. Seriously, don't. 

When writing, do all of the math before you begin writing. The purpose of prose (as opposed to strictly calculations) is to provide necessary and useful context. If you don't know the inputs and results of the calculations are, your prose will be less-than-useful. Furthermore, write the Summary section last. In that section, you'll be pulling details from the other sections. Since you're probably not clarivoyant, this would be difficult to write first. 

## General Notes

1. **Be Concise:** Shorter is better. You want your rec to be as short as possible without sacrificing *necessary* information. 
2. **Be Precise:** Don't say vague things. It (a) signals that you don't knwo what you're talking about and (b) doesn't tell the reader what they need to know. 
3. **Be Correct:** Don't be wrong. If you're unsure about something, ask. 

## Summary

This should be the last section you write. It should almost always be four sentences long (one sentence for each other section), followed by the summary table. 

When filling in the summary table, it may seem like your numbers don't fit the headings. They do. Group all consumption charges (Electricity, Natual Gas, etc) under the "Consumption Savings" heading. If there are multuple types of consumption savings, add both on separate lines. All parts of the implementation cost should be summed before entering them in the table. If a given cell doesn't have a value (including if the payback is immediate), keep the two hyphens. 

Use this template for the summary table: 

```latex

\begin{table}[H]
\centering
\caption{Summary of the savings for AR-\themyAR: XXXXX}
\label{tab:latefees}
\begin{tabular}{ccccc}
\toprule
Consumption Savings & Demand Savings & Annual Savings & Implement.\ Cost & Payback \\
\midrule
-- & -- & -- & -- & -- \\
\bottomrule
\end{tabular}
\end{table}

```

## Current Practices and Observations

## Recommended Action

## Anticipated Savings

## Costs and Payback


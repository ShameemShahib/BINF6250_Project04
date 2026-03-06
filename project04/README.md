# Introduction
In this project, our group implements a de Bruijn graph algorithm for genome assembly. De Bruijn graphs represent sequence overlaps by breaking reads into k-mers, using (k−1)-mers as nodes and overlaps as edges. By constructing the graph and finding an Eulerian path, we can reconstruct the original sequence from fragmented reads. This method is especially effective for handling large, repetitive genomes and high-throughput sequencing data.

# Pseudocode
Put pseudocode in this box:
For our pseudocode, we broke the individual methods down and worked on them one by one.
```
Add_edge
Append the right kmer to the left kmer
{left: [right]}

Remove_edge
Check the left exists and then remove the right 

build_graph_from_reads(ATGCG, k=4)
→ {ATG: [TGC], TGC: [GCG]}
Raise exception if k < 2
Calcualte k-1mer
Loop through each read
	Walk through read by k-1mers
		For each k-1mer → add_edge(left, right)
	
eulerian_walk(node, graph)
Scan through list of dict to find node
Once we find node, record key associated with list
Remove edge with (key, node)
Call the function again using recorded key as the node
Final output would be a list
Reverse list at the end

Assemble_contigs
Build the graph from reads
While dictionary is not empty:
	Scan dictionary for k-1-mer that is in a list but not a key (guarantees it’s at end of a seq)
Do eulerian walk with that k-1-mer
Tour_to_sequence → append to contigs list
Repeat until dictionary is empty

Tour_to_sequence
Take first value of list and append to each remaining kmer

Get_assembly_stats
count the number of contigs
sum up the total length of all contigs
find the longest contig length
find the shortest contig length
calculate the mean length = total length / number of contigs

for N50:
    set threshold = total length / 2
    sort contigs from shortest to longest
    cumulative = 0
    for each contig in sorted order:
        add its length to cumulative
        if cumulative >= threshold:
            n50 = length of this contig

return all stats in a dictionary


Write_fasta
open the output file for writing

for each contig (numbered 1, 2, 3...):
    write a header line: ">Contig_1"
    write the sequence in chunks of 60 characters per line

close the file
```

# Successes
Our collaboration was one of the major successes with our project. We planned out our availability early on so we were able to allocate time to work on the pseudocode and its implementation together. Almost all of our work was done synchronously, which helped us bounce ideas and contribute towards the project. We also spent a significant amount of time on our pseudocode and planning, which made the coding part of our project much easier to tackle.

# Struggles
We did stumble across errors in our code while we were working through each method, but we were able to solve them as they came along. Understanding recursion as a concept was also a challenge for all of us in the group, as well as the Eulerian walk, but we were able to talk through each concept and come to an understanding together. The major challenge we ran into was a memory issue. Trying to run the algorithm for the mouse data took multiple hours (running overnight), and we suspect it had to do with a memory issue slowing down the whole process (didn't even get past the building the graph step). Aside from the memory issue, this might have been slightly improved if we had used a subgraph approach, creating new graphs once nodes were completely disconnected from the ones on the previous graph. However, we conceptually understood the general idea of the algorithm, and even got it working on the toy example which had 10 different overlapping reads. 

# Personal Reflections
## Group Leader
## Shameem
I found the project to be fairly straightforward to understand, and working with my team was a great experience. Our meetings went well ansomething I appreciated was being able to ask questions and help each other stay on the same page. After the last few projects, we all knew the pseudocode needed the most time and energy, and that's exactly where we started. After that stage, the rest went smoothly, and we were all in a meeting whenever code was worked on, which made this project feel the most collaborative for me since barely any work was done asynchronously. Overall, it went really well, and I am happy with the work we produced.

## Other member
## Marcos
While conceptually this project was pretty manageable, getting our algorithm to work with the mouse genome read was much more difficult. We met a few times to discuss the outline of the algorithm, which was very helpful to get organized and understand the concept. During those meetings, we also live-coded the implementation, helping each other with the syntax and different coding techniques. This was very successful for the toy example, where we were able to return the expected aligned contig in a matter of seconds. On the other hand, when assembling the mouse data, just the building of the graph took a very long time (running overnight). We tried to brainstorm ways to optimize the code so it would be faster, and thought that generating subgraphs might have been a good approach. However, this still didn't solve the memory issue we were having, which leads me to think that the way we implemented wasn't the most optimal. Nontheless, I'm happy we got it to work with the toy data, and I really appreciate the work we put in, as it really helped me understand the algorithm.

## Sneha
I enjoyed working with Shameem and Marcos, and I found our meetings to be productive and helpful. I appreciated that we took time to talk through the concepts involved in the project, plan out each of our functions, and write out our pseudocode in the beginning. We all were able to share our ideas to troubleshoot and come up with different approaches. I think this planning made the implementation a lot easier. Everyone was willing to meet to work on the code together, which I found really helpful to be able to talk about our thought processes out loud. In the beginning I was most intimidated by the Eularian walk concept and how to implement it, but after being able to talk with my teammates, ask questions, and implement it together, I feel a lot more confident.

# Generative AI Appendix
As per the syllabus
None was used

# Python Keylogger v2
I've written a keylogger which I intend to use as an Excel study tool, but the captions it generates are displayed only while the corresponding keys are being pressed (terrible design choice!). To solve this problem I propose the following approach:
1. Display the pressed key combinations as comma separated values. For example, instead of first displaying _ctrl + b_, then _ctrl + i_ and finally _ctrl + spacebar_, this key combinations series would be displayed as a a series of three captions with a movable marker (parentheses, for instance). This would be _(ctrl + b)  ctrl + i,   ctrl + spacebar_, then _ctrl + b,  (ctrl + i)  ctrl + spacebar_ and finally _ctrl + b,   ctrl + i,  (ctrl + spacebar)_.
2. The key combinations should be separated by a comma and three white spaces, for instance. This is done to ensure legibility. When the parentheses enclose a given combination, the white space at its left is substituted by a '(', and the comma at its right is substituted by a ')'. This avoids the visually abrupt insertion of parenthesis among combinations. I don't know if I should include some whitespaces at the start and end of the caption, since there will be parentheses there too. This should be tested.
3. We have to set a maximum of key combinations to be displayed in a single caption. I propose a total of five combinations but in principle the code should work for an arbitrary number of combinations.
4. We introduce the concept of _cluster_. We consider a cluster as a time interval in which there are practically no gaps between key combinations. Clusters, along with the key combinations maximum number, serve as criteria for the timestamps of our captions.

## New start and end times

Consider the following diagram.
![image](https://github.com/user-attachments/assets/0bd19b0d-6077-435e-9ff3-95c71abe118e)

This diagram shows the time axis of the interval in which the keylogger is working. The current version of the python keylogger generates a dictionary with the captions (key combinations), index, and start and end times. The start and end times of the i-th caption are then determined by the ordered pair (x_{i,0}, x_{i_f}). To achieve the goals specified in the previous section we need to determine the start and end times of the new captions. This is explained as follows, and **_we assume that we have found the clusters_**.
1. 

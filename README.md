# Divide-Players-Into-Teams-of-Equal-Skill

You are given a positive integer array skill of even length n where skill[i] denotes the skill of the ith player. Divide the players into n / 2 teams of size 2 such that the total skill of each team is equal.

The chemistry of a team is equal to the product of the skills of the players on that team.

Return the sum of the chemistry of all the teams, or return -1 if there is no way to divide the players into teams such that the total skill of each team is equal.

 

Example 1:

Input: skill = [3,2,5,1,3,4]
Output: 22
Explanation: 
Divide the players into the following teams: (1, 5), (2, 4), (3, 3), where each team has a total skill of 6.
The sum of the chemistry of all the teams is: 1 * 5 + 2 * 4 + 3 * 3 = 5 + 8 + 9 = 22.
Example 2:

Input: skill = [3,4]
Output: 12
Explanation: 
The two players form a team with a total skill of 7.
The chemistry of the team is 3 * 4 = 12.
Example 3:

Input: skill = [1,1,2,3]
Output: -1
Explanation: 
There is no way to divide the players into teams such that the total skill of each team is equal.
 

Constraints:

2 <= skill.length <= 105

skill.length is even.

1 <= skill[i] <= 1000

# SOLUTION

Intuition
We are given an array of players' skills, and we need to form teams of two players such that:

All teams have the same total skill.
The chemistry of each team (product of skills) is maximized.
The challenge is to check if it's possible to form such teams and then calculate the total chemistry.

Key observations:
Sorting the array will help us form teams easily.
Pair the smallest player with the largest player.
Check if the sum of skills in each pair is the same.
Approach
Sort the array: Sorting the skills helps in easily forming valid pairs.
Two-pointer approach: Use two pointers—one from the start and one from the end—to pair players. Each pair must have the same total skill.
Check for consistency: If any pair's skill sum differs from the others, return -1.
Calculate chemistry: For valid pairs, calculate the chemistry as the product of the players' skills.
Complexity
Time complexity:
The main operation is sorting the array, which takes (O(n \log n)), where (n) is the length of the array.

Space complexity:
The space complexity is (O(1)), excluding the input array, as we are sorting the array in place and using a constant amount of extra space.

# JAVA CODE

import java.util.Arrays;

class Solution {

    public long dividePlayers(int[] skill) {
    
        // Step 1: Sort the skill array
        
        Arrays.sort(skill);
        
        int n = skill.length;
        
        int totalSkill = skill[0] + skill[n - 1]; // Required sum for each pair
        
        long chemistrySum = 0;

        // Step 2: Pair players using two pointers
        
        for (int i = 0; i < n / 2; i++) {
        
            // Check if the sum of current pair matches the required totalSkill
            
            if (skill[i] + skill[n - i - 1] != totalSkill) {
            
                return -1; // Invalid configuration, return -1
            }
            // Calculate the chemistry (product of pair) and add it to the sum
            
            chemistrySum += (long) skill[i] * skill[n - i - 1];
        }

        return chemistrySum; // Return total chemistry
        
    }
    
}

Step-by-Step Detailed Explanation
Sorting the array:
We sort the skill[] array to ensure that the smallest player can be paired with the largest player. Sorting helps us form pairs that are easy to check for total skill consistency.

Two-pointer pairing:
We initialize two pointers:

One (i) starts from the beginning of the array.
The other (j) starts from the end of the array.
These two pointers move toward each other, forming pairs of players.

Checking pair consistency:
For each pair of players, we check if their total skill equals the required sum (the total skill of the first and last player). If any pair fails this check, it is impossible to divide the players into valid teams, and we return -1.

Calculating chemistry:
If all pairs are valid, we compute the "chemistry" of each team as the product of the players' skills. We sum up these chemistry values to get the final result.

Returning the result:
If we successfully form all the teams, we return the sum of the chemistry. If not, we return -1.

Visualization:
Suppose we are given the following skill array:

skill = [3, 2, 5, 1, 3, 4]
Step 1: Sort the array
We begin by sorting the array to simplify pairing the smallest with the largest:

Sorted skill array = [1, 2, 3, 3, 4, 5]
Step 2: Form teams
We use two pointers:

One pointer starts at the beginning of the array (i = 0),
The other starts at the end (j = length - 1).
We form pairs as follows:

Pair #	Player 1 (Left Pointer i)	Player 2 (Right Pointer j)	Total Skill
1	1	5	6
2	2	4	6
3	3	3	6
Step 3: Verify skill sum
The total skill for each pair is 6, which is consistent across all pairs. This confirms that we can divide the players into valid teams.

Step 4: Chemistry calculation
The "chemistry" of each team is the product of the players' skills. Let's calculate the chemistry for each pair:

Pair #	Player 1	Player 2	Chemistry (Product)
1	1	5	1 * 5 = 5
2	2	4	2 * 4 = 8
3	3	3	3 * 3 = 9
The total chemistry sum is:

5 + 8 + 9 = 22
Visual Representation:
Players sorted by skill: [1, 2, 3, 3, 4, 5]

1st Pair: (1, 5) -> Chemistry: 1 * 5 = 5
2nd Pair: (2, 4) -> Chemistry: 2 * 4 = 8
3rd Pair: (3, 3) -> Chemistry: 3 * 3 = 9

Total Chemistry: 5 + 8 + 9 = 22
Invalid Example:
For the array:

skill = [1, 1, 2, 3]
After sorting:

Sorted skill array = [1, 1, 2, 3]
We try to form pairs:

Pair #	Player 1	Player 2	Total Skill
1	1	3	4
2	1	2	3
The total skill for the first pair is 4 and for the second pair is 3. Since the total skill differs, it is impossible to form valid teams. Hence, we return -1.

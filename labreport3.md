# Part 1 - Bugs
## A failure-inducing input for the buggy program
```
	@Test
	public void testReversed2() {
		int[] input1 = {1, 2, 3};
		assertArrayEquals(new int[]{3, 2, 1}, ArrayExamples.reversed(input1));
	}
```
## An input that doesn’t induce a failure
```
	@Test
	public void testReversed() {
		int[] input1 = { };
		assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
	}
```
## The symptom

![Image](trat.png)

## The bug
### Before
```
	static int[] reversed(int[] arr) {
		int[] newArray = new int[arr.length];
		for(int i = 0; i < arr.length; i += 1) {
			arr[i] = newArray[arr.length - i - 1];
		}
		return arr;
	}
```
### After
```
	static int[] reversed(int[] arr) {
		int[] newArray = new int[arr.length];
		for(int i = 0; i < arr.length; i += 1) {
			newArray[i] = arr[arr.length - i - 1];
		}
		return newArray;
	}
```

The symptom shows that the array for some reason sets the first element to 0, which is an element that is not in the given array. The error is that the original code edits ``arr`` with the values of ``newArray`` instead of the reverse, and it also returns ``arr`` which is incorrect as it's supposed to return a new array. This explains the first element being 0 as new integer arrays are filled with all zeros.

# Part 2 - Researching Commands (grep)
**All command-line options listed here were found on the [man page](https://man7.org/linux/man-pages/man1/grep.1.html), here is a link**

## grep -v
### Example 1
```
λ grep -v "an" pmed.0020226.txt





        Richard Smith's key suggestion [1] is that medical journals “should stop publishing
        vehicles for scientific information, but it's unclear what will save them. Even as journals


```
### Example 2
```
λ grep -v "avighna" pmed.0020191.txt





        The excellent article by Jordan Paradise, Lori B. Andrews, and colleagues, “Ethics.
        Constructing Ethical Guidelines for Biohistory” [1], neither advocates nor argues against
        biohistorical research; instead, it points out that such investigations are currently
        taking place without guidelines—ethical, scientific, moral, or religious. The question
        remains: if such guidelines were to be established, what individuals, institutions,
        governments, medical examiners, family members, or intrepid biographers are to be given
        permission? Who is to decide what is “historically significant”? Not to mention the
        meta-question: who is to decide who is to decide? I apologize to the authors if my brief
        comments [2] implied that they took a position on this issue.


```
The -v flag will inverse the search. If a line does not contain the given string, then it will print the line. The second example shows that if the given string is not in any of the lines, it will just print all of the lines. This is great as it can help cut down on useless info in a file to search for the actually useful information.

## grep -i
### Example 1
```
λ grep -i "in" pmed.0020192.txt
        I am writing in response to an essay published in the most recent issue of
        PLoS Medicine by Deborah Hayden, entitled “Alas, Poor Yorick: Digging Up
        by her comment on our article. Nowhere in that article, “Ethics. Constructing Ethical
        Guidelines for Biohistory” [2], do we suggest that genetic testing be done on deceased
        individuals for historically significant questions? In fact, we specifically highlight some
        of the ethical, legal, social, and scientific issues that such testing raises and recommend
        that guidelines be developed in order to monitor current research that is being undertaken
        in this area. The article does not advocate biohistorical research. This distinction is
        very important and one that is quite evident upon a careful reading of our article.
```
### Example 2
```
λ grep -i "IN" pmed.0020048.txt
        Current journal requirements forcing clinical trials to be registered [1] are
        insufficient and are unlikely to solve the problem of negative trials never even making it
        to a journal. Most of the patients consenting to clinical trials do so out of altruism. It
        is a great betrayal of their trust to suppress clinical trial data. I suggest that
        institutional review boards refuse to allow human experimentation unless the protocol is
        filed in a central (online) repository. The primary data should also be required to be in
        the public domain (say, within 1–2 years after completion). Data obtained by appealing to
        altruistic instincts, similar to money in public charities, are not proprietary
        information, nor can physicians cash out the trust of their patients. In reality, it is the
        pharmaceutical industry that stands to gain the most if data are made public as such data
        inform future research and help smaller, innovative companies avoid redundancy. Voluntarily
        sticking to higher standards of ethics will raise societal respect for the industry
        (currently being battered for greed) attract a more talented workforce, and may even
```
The -i flag will check without caring about the case. Either way, if given lowercase (like Example 1) or uppercase (like Example 2), 

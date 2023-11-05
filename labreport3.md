# Part 1 - Bugs
## A failure-inducing input for the buggy program, as a JUnit test and any associated code
```
	@Test
	public void testReversed2() {
		int[] input1 = {1, 2, 3};
		assertArrayEquals(new int[]{3, 2, 1}, ArrayExamples.reversed(input1));
	}
```
## An input that doesn’t induce a failure, as a JUnit test and any associated code
```
	@Test
	public void testReversed() {
		int[] input1 = { };
		assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
	}
```
## The symptom, as the output of running the tests

![Image](trat.png)

## The bug, as the before-and-after code change required to fix it
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

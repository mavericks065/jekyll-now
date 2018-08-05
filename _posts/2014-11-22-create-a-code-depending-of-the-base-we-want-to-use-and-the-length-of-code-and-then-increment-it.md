---
layout: post
title: Create unique code with a determined base
---
I wanted to create a unique code that was readable which means different from what you get when you use UUID or anything else. And it was also necessary to increment this code every time a new document was created.

My requirement was to create a code that will identify a document and for the clients it had to be readable and can be incremental. Depending the type of document, the code would be in base 16 / 36 / 4 / 10 or whatever and the length of the code 4/5/6/8 characters.

Here is my code : (any commentary is welcome)

```java
private String computecodeNumber(final int base, final int numDigits, int lastCodeInt) throws Exception {

	// can't compute something that is not in our specs
	if (base > baseMax) {
		throw new IllegalArgumentException(" base : " + base + " is superior than the maximum base : " + baseMax);
	}

	String lastCode = Integer.toString(lastCodeInt, base);
	final List<Character> baseCharacters = charsForBase.subList(0, base-1);

	// just checking if lastCode has been initialized and use if not it creates it
	if (lastCode == null || lastCode.isEmpty()) {
		StringBuffer sb = new StringBuffer();
		for (int i = 0; i < numDigits; i++) {
			sb.append("0");
		}
		return sb.toString();
	} else if (lastCode.length() != numDigits) {
		throw new Exception(" past existing code length is " + lastCode.length() + " and is not equals to what we expect : " + numDigits);
	}

	// we parse our String we have the good base then increment then we get it back in String
	int codeInt = Integer.parseInt(lastCode, base);
	codeInt++;
	return Integer.toString(codeInt, base);
}
```


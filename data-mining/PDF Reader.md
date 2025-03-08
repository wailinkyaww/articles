# Comprehensive Guide to Choosing a PDF Reader for your next GenAI Application


PDF - it is a billion-dollar mistake that I would name even in my dream.

From students to legal documents, startups to enterprise, PDF is the most widely used format when it comes to sharing unstructured information.
As much as it is useful and widely adopted, the cost that we are paying for it to integrate with other tools & technologies - like GenAI is just spiking up.

I’ve tested libraries, third party services, and even implemented custom solutions on my own. <br />
None of these gives me a satisfactory result.

Today I am going to share the trade-offs between all these libraries. <br />
What works, what doesn’t, and how to pick a good enough solution for your use case.

## Understanding PDF Representation

Before we talk about the libraries, let's dive into what are the inherent issues with the PDF itself. <br />
PDF internal representation favors the portability across digital platforms - android, iOS, Window, Mac, Linux, etc.,

It's designed to solely rely on cartesian ( x / y ) coordinates system, whether it is
- rendering text
- spaces
- line breaks
- even visual elements ( e.g., tables borders )


### Text & Spaces

Say we want to render this piece of text - "quick fox jumps dog", <br />
we can represent as following.
```json
{ "text": "quick fox jumps dog", "x": 0, "y": 0 }
```

<img src="../assets/PDF/good-representation.png" style="border-radius: 5px;" width="500" />

At first, the use of ( x / y ) seems perfectly fine.  Let's see another example.
```ts
// Just assume each word has the same length for this example
[{ "text": "quick", "x": 0, "y": 0, "width": 0.5, "height": 0.3 }
,{ "text": "fox",   "x": 1, "y": 0, "width": 0.5, "height": 0.3 }
,{ "text": "jumps", "x": 2, "y": 0, "width": 0.5, "height": 0.3 }
,{ "text": "dog",   "x": 3, "y": 0, "width": 0.5, "height": 0.3 }
]
```

Nothing is preventing someone to represent the same text with this new structure. <br />
This will result in the same visual representation at the end user perspective.

If you look closely, there is no **space** in any of these the block.

So, how would you  get the same result?? <br />
➡️ **x / y coordinates offset**

Take a look at the following image.

<img src="../assets/PDF/bad-presentation.png" style="border-radius: 5px;" width="500" />

People can just do the same for other important building blocks like new lines, column layouts, tables etc.,

### Natural Reading Order

In English, we read from top to bottom, left to right. <br/>
In arabic, urdu, and middle east languages, we read from left to right, top to bottom. <br />
In Chinese, Japanese, and Korean languages also have vertical writing system where we have to read from top to bottom first, then left to right. <br />

PDF internal representation doesn't enforce the natural reading order. <br />
We can write down the text and ( x / y ) coordinates pairs in any order regardless of their position in the page. <br />

```ts
[{ "x": 0, "y": 1, "text": "header" } // item 1
,{ "x": 0, "y": 2, "text": "paragraph 1" } // item 2
,{ "x": 0, "y": 3, "text": "paragraph 2" } // item 3
,{ "x": 0, "y": 4, "text": "footer" } // item 4
]
```

Above example is the ideal representation. It shows that the representation follows our reading order.
However, one could also just footer block in place of `Item 1` and get the same result.

Here, I am talking about top to bottom structure.
This also applies left to right text elements.

A simple way to fix this problem is to sort the text blocks (in case of English)
- top to bottom, sort by y coordinates
- then left to right, sort by x coordinates

Most PDF reader libraries don't have this.

However, simple sorting will not work if your document contains 
- other elements like tables embedded in the middle of text
- multi column layouts

We have two options here to detect the layout.
1. use the algorithmic approach (will not cover all the edge cases)
2. use deep learning models to detect the layout, the combine with algorithmic approach
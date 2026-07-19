---
name: prose-revision
description: Prose for a human reader is the deliverable. Use when writing or revising anything a person will sit and read, including docs, READMEs, PR descriptions, site copy, posts, emails, and UI text. Not for code, commit messages, or chat replies.
---

# Prose Revision

A language model writes from a context the reader does not have, in phrases it has seen a million times. Left alone, the output is waffle: pre-assembled, abstract, padded. This skill is the revision pass that strips it.

## The five

1. **Concrete beats abstract.** Nouns and verbs carry the sentence. "More people died", not "mortality rose". A reached-for adverb is a weak verb's symptom: fix the verb.
2. **Cut what the reader already has.** Compression targets redundancy with what the reader knows, not word count. A useful target: second draft = first draft minus ten percent.
3. **No pre-assembled phrases.** If the phrase arrived whole ("it's important to note", "seamlessly", "in today's fast-paced world"), it goes. The escape from a cliché is the literal statement, not a fresher metaphor. A metaphor earns its place twice: by being fresh, and by being clearer than the plain sentence it replaces. Otherwise delete it, do not upgrade it.
4. **Show the thing, don't label the reaction.** Do not call it "powerful", "delightful", or "robust"; describe it so the reader says that. Adjectives that tell the reader how to feel are you doing their reading for them.
5. **The override.** When any rule fights clarity, clarity wins. In doubt between plain and clever, choose plain.

## The pass

Draft freely first; prose composed under these rules comes out stilted. Then revise:

1. Bracket every word not doing useful work. Delete each bracket you cannot defend.
2. Per sentence: what am I trying to say? Do these words say it? Could I put it more shortly?
3. Read it as the reader, who does not have your context. Codenames invented mid-task, shorthand from the work, conclusions without the evidence: expand or cut.

## Not Hemingway

Overcorrected prose fails the same test flabby prose fails.

- Flabby: "It is important to note that the deployment process can take a significant amount of time."
- Overcorrected: "Deploys: slow."
- Right: "Deploys take about ten minutes."

The passive is correct when the object is the point: "the config is loaded before routes register", because the loader is nobody. An adverb that changes meaning stays ("silently fails"); an adverb that adds volume goes ("very quickly" means find a faster verb). Vary sentence length. A paragraph of uniform short sentences reads like a telegram, and that is a costume too.

## Where it does not apply

Code, commit messages, comments, chat replies, terminal output: those want boring convention. And anything in the human's own voice, such as a draft they will reword, keeps their voice. Suggest, don't sand.

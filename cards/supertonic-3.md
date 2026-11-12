---
license: openrail++
---

# supertonic-3

Supertone's Supertonic-3 multilingual text-to-speech, as FluidInference converted it to Core ML
(`FluidInference/supertonic-3-coreml` at `9f3606bf5c5ff9d6680cf6226614ac61358a24f3`, card `license: openrail++`),
modified by ac so its three VectorEstimator buckets share one weight file. Loaded by FluidAudio 0.16.1
(`Supertonic3Manager`, `.aneBucketed(.int4)`) on macOS and iOS.

**Licence:** BigScience OpenRAIL-M, Supertone's (`Supertone/supertonic-3` at
`3cadd1ee6394adea1bd021217a0e650ede09a323`), carried verbatim in the asset as `LICENSE`. Its use
restrictions (Attachment A, below) bind every use of these files and of anything derived from them;
whoever redistributes them or a derivative must pass the same restrictions on.

## The modification

`VectorEstimatorVariants/VectorEstimator_L{128,256,512}_int4.mlmodelc` are one network at three fixed
lengths. Each keeps its own program; each `model.mil` reads its weights at new offsets in ONE weight file
holding every distinct blob of the three originals once, byte for byte (448 blobs, 32,169,472 B). The asset
holds that file at `VectorEstimator_L128_int4.mlmodelc/weights/weight.bin` and the other two buckets'
`weights/weight.bin` as tar hard links to it, so it is on disk once. No weight value was changed; every other
file is FluidInference's, unchanged. Each bucket is bit-exact with its original on CPU_ONLY (ac's
`dist/voice-parity/supertonic-3-vector-estimator.json`). The asset's `NOTICE.md` says the same.

## Use restrictions (OpenRAIL-M, Attachment A, verbatim)

You agree not to use the Model or Derivatives of the Model:
(a) In any way that violates any applicable national, federal, state, local or international law
or regulation;
(b) For the purpose of exploiting, harming or attempting to exploit or harm minors in any
way;
(c) To generate or disseminate verifiably false information and/or content with the purpose of
harming others;
(d) To generate or disseminate personal identifiable information that can be used to harm an
individual;
(e) To generate or disseminate information and/or content (e.g. images, code, posts, articles),
and place the information and/or content in any context (e.g. bot generating tweets)
without expressly and intelligibly disclaiming that the information and/or content is
machine generated;
(f) To defame, disparage or otherwise harass others;
(g) To impersonate or attempt to impersonate (e.g. deepfakes) others without their consent;
(h) For fully automated decision making that adversely impacts an individual’s legal rights or
otherwise creates or modifies a binding, enforceable obligation;
(i) For any use intended to or which has the effect of discriminating against or harming
individuals or groups based on online or offline social behavior or known or predicted
personal or personality characteristics;
(j) To exploit any of the vulnerabilities of a specific group of persons based on their age,
social, physical or mental characteristics, in order to materially distort the behavior of a
person pertaining to that group in a manner that causes or is likely to cause that person or
another person physical or psychological harm;
(k) For any use intended to or which has the effect of discriminating against individuals or
groups based on legally protected characteristics or categories;
(l) To provide medical advice and medical results interpretation;
(m) To generate or disseminate information for the purpose to be used for administration of
justice, law enforcement, immigration or asylum processes, such as predicting an
individual will commit fraud/crime commitment (e.g. by text profiling, drawing causal
relationships between assertions made in documents, indiscriminate and
arbitrarily-targeted use).

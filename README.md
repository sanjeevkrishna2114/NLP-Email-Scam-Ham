# NLP-Email-Scam-Ham
Trying to classify as scam or ham using NLP techniques and comparing 3 different approaches


## We have tried three different approaches here

## Three-Pipeline Architecture

### 1. URL & Header Analysis (Fast Filter)
Extracts structural signals from the email using RegEx — URL length, subdomain depth, sender/receiver domain mismatch, and blacklist lookups. Aggregates these into a suspicion score and applies a threshold to immediately flag obvious scams **without running any model**.

### 2. Bi-LSTM + Embeddings (Semantic Understanding)
Preprocesses text (tokenization, lowercasing) and converts words into dense vectors using Word2Vec / fastText / Doc2Vec. A **Bi-LSTM** reads the email bidirectionally to capture sequential context — understanding that "account suspended + click here + immediately" together signal scam, not just individually. The hidden state is fused with TF-IDF features before a final Dense FCN + Sigmoid classifier.

### 3. TF-IDF / Bag of Words (Statistical Classification)
Encodes emails using corpus-aware frequency weighting. TF-IDF explicitly amplifies rare but highly discriminative scam words (e.g. "lottery", "wire transfer", "urgent payment") that a sequential model might dilute. Fed directly into a Dense FCN + Sigmoid classifier.

---

## Why Three Pipelines?

Each approach catches what the others miss — structural URL signals, deep semantic context, and sharp statistical keyword weights. The **feature-level fusion** of Pipelines 2 and 3 (concatenating Bi-LSTM hidden state + TF-IDF vector) combines contextual and corpus-level signals for the final classification decision.

---

## Team

Krishna Cheliaah S · S Sanjeev Krishna · Siddid Soni  
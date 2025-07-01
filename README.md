
# Step-by-Step Instructions to Build a Q&A Chatbot (Lex + Bedrock + S3)

## Summary

This project demonstrates how to build a Q&A chatbot using Amazon Lex V2, Amazon Bedrock, and Amazon S3. The bot can understand user inputs, fetch answers from a knowledge base built from documents stored in S3, and respond using pre-configured intents. It uses Titan Embeddings for semantic search and Claude for language understanding.

## Step 1: Prepare Your Documents

1. Go to Amazon S3.
2. Create a new bucket (enter a name of your choice).
3. Upload `.docx`, `.pdf`, or `.txt` documents (e.g., terms, policies, manuals).
4. Keep the bucket private.
5. Note the bucket name and path.

## Step 2: Create a Knowledge Base (Amazon Bedrock)

1. Go to the Amazon Bedrock console → Knowledge bases.
2. Click "Create knowledge base".
3. Enter:
   - Name: (enter any name)
   - Embeddings model: Titan Embeddings G1 - Text
   - RAG model: Claude v2 or latest version
4. Select Amazon S3 as your data source.
5. Point to the bucket and folder where your documents are stored.
6. Leave other settings as default.
7. Click "Create" and wait for indexing to complete.

## Step 3: Create an Amazon Lex V2 Bot

1. Go to Amazon Lex V2 → Bots → Create bot.
2. Configure:
   - Name: (enter any name)
   - IAM Role: Let Lex create or select a role with S3 and Bedrock access
   - Data Privacy: Accept defaults
   - Child-Directed: Select No
3. Click "Next" and complete the bot creation.

## Step 4: Configure Intents

### 4.1 Welcome Intent

1. Create a new intent (enter name of your choice).
2. Add sample utterances:
   - hi
   - hello
3. Add a response:
   ```
   What can I do for you?
   ```
4. Under Advanced Settings, enable:
   - Wait for user input
5. Save the intent.

### 4.2 QnA Intent (Knowledge Base)

1. Click "Add intent" → Choose "Pre-built" → Select "QnAIntent"
2. Link it to the knowledge base created in Step 2.
3. Save the intent.

## Step 5: Build and Test the Bot

1. Click "Build" (top-right).
2. After the build finishes, open the Test Bot panel.
3. Try:
   - Saying hi or hello → Bot replies "What can I do for you?"
   - Asking a question from your documents → Bot replies accurately
   - Asking something unrelated → Bot triggers fallback intent

## Tech Stack

- Amazon Lex V2 for building and deploying the chatbot
- Amazon Bedrock for semantic understanding and knowledge base support
- Claude (Anthropic) model for language generation
- Titan Embeddings G1 - Text for vector search
- Amazon S3 for document storage
- Pre-built QnAIntent and custom intent logic in Lex

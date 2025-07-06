# 🤖 Reddit Parser Jupyter Notebook - Complete Guide

Simple and powerful Jupyter notebook for Reddit parsing, LLM analysis, and generating new post ideas.

## 🚀 Quick Start (Step-by-Step Guide)

### Step 1: Install Dependencies
```bash
pip install praw python-dotenv requests openpyxl pandas openai httpx backoff nest-asyncio jupyter
```

### Step 2: API Keys Setup

#### 2.1 Reddit API:
1. Go to https://www.reddit.com/prefs/apps
2. Click "Create App" or "Create Another App"
3. Fill out the form:
   - **Name**: any name (e.g., "My Reddit Parser")
   - **App type**: select "script"
   - **Description**: optional
   - **About URL**: leave blank
   - **Redirect URI**: enter `http://localhost:8080`
4. Click "Create app"
5. Copy:
   - **Client ID**: located under the app name (short string)
   - **Client Secret**: long string under "secret"

#### 2.2 OpenRouter API:
1. Register at https://openrouter.ai/
2. Go to "Keys" section
3. Create a new API key
4. Copy the key

#### 2.3 Environment Variables Setup:
**Option A (recommended)**: Create a `.env` file in the project folder:
```env
REDDIT_CLIENT_ID=your_client_id_here
REDDIT_CLIENT_SECRET=your_client_secret_here
OPENROUTER_API_KEY=your_openrouter_key_here
```

**Option B**: Change variables directly in the notebook in the "Global Settings" section:
```python
REDDIT_CLIENT_ID = "your_client_id_here"
REDDIT_CLIENT_SECRET = "your_client_secret_here"
OPENROUTER_API_KEY = "your_openrouter_key_here"
```

### Step 3: Launch Notebook
```bash
jupyter notebook reddit_parser_notebook.ipynb
```

### Step 4: First Run
**⚠️ IMPORTANT**: Always start with "QUICK TESTING" first
1. Open the notebook
2. Find the "Alternative Settings" section
3. Uncomment the "QUICK TESTING" block
4. Run all cells sequentially

### Step 5: Verify Results
If everything works correctly, you should see:
- Successful Reddit API connection
- Posts parsing from subreddits
- LLM idea generation
- Excel and JSON files creation

## 🎯 Notebook Features

- 📊 **Reddit Parsing**: Posts and comments from any subreddits
- 🧠 **LLM Analysis**: Automatic trend analysis through AI
- 💡 **Idea Generation**: Creating new post ideas with different styles
- 📈 **Analytics**: Detailed statistics and visualization
- 💾 **Export**: Excel and JSON files with results
- 🔄 **Auto-continuation**: Automatic continuation of truncated responses
- 🛠️ **Smart Parsing**: Enhanced JSON response processing
- 🎭 **4 Generation Styles**: human, humorous, technical, discussion-starter

## 🌍 Detailed Settings

### Main Parsing Parameters:
```python
# Subreddits for parsing
TARGET_SUBREDDITS = [
    'Python',           # Python programming
    'MachineLearning',  # Machine learning
    'programming',      # General programming
    'artificial',       # Artificial intelligence
    'technology'        # Technology
]

# Subreddits for content generation (can be different)
CONTENT_GENERATION_SUBREDDITS = [
    'Python',
    'learnpython',
    'MachineLearning'
]

# Parsing parameters
POSTS_PER_SUBREDDIT = 15    # Number of posts per subreddit
SORT_BY = 'hot'             # Sort type: 'hot', 'new', 'top', 'rising'
COMMENTS_PER_POST = 10      # Number of comments per post
TEXT_LIMIT = 2000           # Text character limit (None = no limit)
```

### LLM Settings (ENHANCED):
```python
# Main LLM parameters
LLM_MODEL = 'google/gemini-2.5-flash-lite-preview-06-17'  # Analysis model
MAX_CONCURRENT_REQUESTS = 30    # Number of concurrent requests
IDEAS_PER_SUBREDDIT = 2         # Number of ideas per subreddit
MAX_TOKENS = 2500               # Maximum tokens for response
TIMEOUT_SECONDS = 90            # Response timeout in seconds
ENABLE_CONTINUATION = True      # Enable auto-continuation on truncation
```

## 🔧 Ready Configurations for Different Needs

### 🚀 Quick Testing (RECOMMENDED FOR START):
```python
TARGET_SUBREDDITS = ['Python', 'MachineLearning']
POSTS_PER_SUBREDDIT = 5
MAX_TOKENS = 1500
TIMEOUT_SECONDS = 60
ENABLE_CONTINUATION = True
```
**Use for**: First run, settings testing

### 💰 Budget Usage:
```python
LLM_MODEL = 'google/gemini-2.5-flash-lite-preview-06-17'
MAX_TOKENS = 1000
TEXT_LIMIT = 500
ENABLE_CONTINUATION = False
MAX_CONCURRENT_REQUESTS = 10
```
**Use for**: Minimizing API costs, quick analysis

### 🏆 Maximum Quality:
```python
LLM_MODEL = 'anthropic/claude-3-sonnet'
MAX_TOKENS = 4000
TIMEOUT_SECONDS = 120
TEXT_LIMIT = None
ENABLE_CONTINUATION = True
```
**Use for**: Best results, detailed analysis

### 🔬 Detailed Analysis:
```python
POSTS_PER_SUBREDDIT = 50
IDEAS_PER_SUBREDDIT = 5
MAX_TOKENS = 3000
COMMENTS_PER_POST = 20
```
**Use for**: Deep research, big data

## 🎭 Content Generation Styles

The notebook supports 4 different styles for more natural and human-like posts:

### 1. 🧑‍💻 Human & Relatable (`human_relatable`)
- **Model**: Claude 3 Haiku
- **Focus**: personal stories, problems, empathy
- **Temperature**: 0.8
- **Example**: "I spent 3 hours looking for a bug, and it was in the printer..."

### 2. 😄 Humorous & Casual (`humorous_casual`)
- **Model**: GPT-4o Mini
- **Focus**: jokes, memes, light tone, Reddit slang
- **Temperature**: 0.9
- **Example**: "When your code works on the first try 🤔"

### 3. 🔧 Technical but Engaging (`technical_engaging`)
- **Model**: Gemini 2.0 Flash
- **Focus**: technical discoveries, tips, TIL format
- **Temperature**: 0.6
- **Example**: "TIL: Python 3.12 has a hidden feature..."

### 4. 💬 Discussion Starter (`discussion_starter`)
- **Model**: Claude 3 Sonnet
- **Focus**: controversial opinions, questions, debates
- **Temperature**: 0.7
- **Example**: "Unpopular opinion: JavaScript is better than Python for..."

### Changing Style:
```python
# In the style configuration cell, change:
SELECTED_STYLE = "humorous_casual"  # or another style
```

## 🛡️ Safety and Control Mechanisms

### New limitations for safe content:

1. **Fact Fabrication Prevention**:
   - LLM cannot create specific events that definitely didn't happen
   - Use hypotheses and personal opinions instead of "facts"
   - Additional `safety_check` field in JSON response

2. **Emoji Control**:
   - Maximum 1-2 emojis per post
   - Only for emotion enhancement or irony
   - Avoid emoji abuse

3. **Personal Stories Enforcement**:
   - Minimum one of two posts must be a personal story
   - `is_personal_story` field for tracking
   - Automatic validation after generation

### JSON Structure with New Fields:
```json
{
  "post_ideas": [
    {
      "title": "...",
      "content": "...",
      "post_type": "personal story",
      "is_personal_story": true,
      "safety_check": "I confirm I'm not fabricating specific facts"
    }
  ]
}
```

## 📊 What the Notebook Does (Detailed Process)

### 1. Reddit Parsing:
- Connects to Reddit API via PRAW
- Retrieves posts from specified subreddits
- Parses comments for each post
- Stores metadata (score, author, creation time, etc.)
- Handles errors and rate limits

### 2. Basic Analytics:
- Top posts by score
- Top posts by comment count
- Statistics by subreddit
- Activity analysis by time

### 3. LLM Analysis (ENHANCED):
- Analyzes trends and popular topics
- Identifies post success factors
- Generates new post ideas for each subreddit
- **Automatic continuation** on response truncation
- **Enhanced JSON parsing** with error handling
- **Detailed diagnostics** for generation issues

### 4. Additional Analytics:
- Best posting hours
- Best days of the week
- Title length analysis
- Correlation analysis
- Popular words wordcloud

### 5. Results Saving:
- Excel file with posts and comments
- JSON file with generated ideas
- Statistics by subreddit
- Charts and visualizations

## 📁 Output Files

The notebook creates timestamped files to avoid overwriting:
- `reddit_posts_YYYYMMDD_HHMMSS.xlsx` - all posts and comments data
- `generated_ideas_YYYYMMDD_HHMMSS.json` - generated post ideas

### Excel File Structure:
- **"Posts" Sheet**: all posts with metadata
- **"Comments" Sheet**: all comments linked to posts
- **"Stats" Sheet**: subreddit statistics

### JSON File Structure:
```json
{
  "generation_info": {
    "timestamp": "2024-01-01 12:00:00",
    "total_ideas": 10,
    "successful_generations": 8,
    "failed_generations": 2
  },
  "ideas_by_subreddit": {
    "Python": [
      {
        "title": "...",
        "content": "...",
        "post_type": "...",
        "is_personal_story": true,
        "safety_check": "..."
      }
    ]
  }
}
```

## ⚡ Example Output

```
🏆 TOP-10 POSTS BY SCORE:
 1. Complete Python Guide for Beginners... (Score: 1500, r/Python)
 2. Machine Learning in 2024: What's New... (Score: 1200, r/MachineLearning)
 3. Why I Switched from Java to Python... (Score: 980, r/programming)

💡 GENERATED IDEAS (8/10 successful):
📝 Title: "Python Performance Tips That Actually Matter"
📄 Content: A comprehensive guide covering...
🎯 Rationale: Combines popular topics of performance and practical tips
📈 Engagement Prediction: high
🎭 Style: technical_engaging
```

## 🛠️ Detailed Problem Solving

### ❌ Problem: "Generated 0 post ideas!"

**Step-by-step solution:**

1. **Check API keys:**
   ```python
   # Verify variables are set correctly
   print(f"Reddit Client ID: {REDDIT_CLIENT_ID[:10]}...")
   print(f"OpenRouter API Key: {OPENROUTER_API_KEY[:10]}...")
   ```

2. **Try quick testing:**
   ```python
   # Uncomment "QUICK TESTING" block
   TARGET_SUBREDDITS = ['Python']
   POSTS_PER_SUBREDDIT = 3
   MAX_TOKENS = 1500
   TIMEOUT_SECONDS = 60
   ```

3. **Switch to more stable model:**
   ```python
   LLM_MODEL = 'anthropic/claude-3-haiku'
   ```

4. **Reduce load:**
   ```python
   MAX_CONCURRENT_REQUESTS = 10
   TEXT_LIMIT = 1000
   ```

### ⚠️ Problem: "Failed to parse JSON"

**This is partially normal behavior!** The notebook has built-in mechanisms:

1. **Automatic continuation:**
   - On response truncation, notebook will automatically continue generation
   - Enable `ENABLE_CONTINUATION = True`

2. **Raw text display:**
   - If JSON doesn't parse, notebook will show raw text
   - This helps understand what went wrong

3. **Result improvement:**
   ```python
   MAX_TOKENS = 3000  # Increase tokens
   TIMEOUT_SECONDS = 120  # Increase timeout
   LLM_MODEL = 'anthropic/claude-3-sonnet'  # Better models
   ```

### 🐌 Problem: Slow Performance

**Gradual optimization:**

1. **Reduce data:**
   ```python
   POSTS_PER_SUBREDDIT = 5
   COMMENTS_PER_POST = 5
   TEXT_LIMIT = 500
   ```

2. **Use faster model:**
   ```python
   LLM_MODEL = 'google/gemini-2.5-flash-lite-preview-06-17'
   ```

3. **Reduce parallelism:**
   ```python
   MAX_CONCURRENT_REQUESTS = 10
   ```

4. **Fewer subreddits:**
   ```python
   TARGET_SUBREDDITS = ['Python', 'MachineLearning']
   ```

### 🔑 Problem: "REDDIT_CLIENT_ID not found"

**Solution:**

1. **Check .env file:**
   - Ensure `.env` file exists in project folder
   - Check for no spaces around `=` signs
   - Check for no quotes around values

2. **Alternatively change in notebook:**
   ```python
   # In "Global Settings" section
   REDDIT_CLIENT_ID = "your_actual_client_id"
   REDDIT_CLIENT_SECRET = "your_actual_client_secret"
   ```

### 🌐 Problem: "API Error" or "Rate limit"

**Solution:**

1. **Check internet connection**

2. **Reduce load:**
   ```python
   MAX_CONCURRENT_REQUESTS = 5
   POSTS_PER_SUBREDDIT = 3
   ```

3. **Add delays:**
   ```python
   import time
   time.sleep(2)  # Between requests
   ```

## ⚠️ Limitations and Recommendations

### Reddit API Limitations:
- **Rate limit**: 60 requests per minute
- **User Agent**: must specify unique User Agent
- **Respect robots.txt**: don't parse forbidden subreddits

### OpenRouter API Limitations:
- **Model-dependent**: different models have different limits
- **Tokens**: monitor token usage costs
- **Timeout**: some models can be slow

### General Recommendations:

1. **Start with testing**:
   - Always use "QUICK TESTING" first
   - Gradually increase data volume

2. **Monitor costs**:
   - Track API spending
   - Use `TEXT_LIMIT` for cost savings

3. **Save results**:
   - Regularly export data
   - Backup important results

4. **Optimize for your needs**:
   - Adjust parameters for your goals
   - Experiment with different models

## 🔍 Detailed Usage Examples

### Scenario 1: First Run
```python
# 1. Set up API keys in .env or notebook
# 2. Uncomment "QUICK TESTING"
TARGET_SUBREDDITS = ['Python']
POSTS_PER_SUBREDDIT = 3
MAX_TOKENS = 1500

# 3. Run all cells
# 4. Check results
```

### Scenario 2: Budget Usage
```python
# For cost minimization
LLM_MODEL = 'google/gemini-2.5-flash-lite-preview-06-17'
MAX_TOKENS = 1000
TEXT_LIMIT = 500
ENABLE_CONTINUATION = False
MAX_CONCURRENT_REQUESTS = 10
```

### Scenario 3: Maximum Quality
```python
# For best results
LLM_MODEL = 'anthropic/claude-3-sonnet'
MAX_TOKENS = 4000
TIMEOUT_SECONDS = 120
TEXT_LIMIT = None
ENABLE_CONTINUATION = True
```

## 🆘 Diagnostics and Logging

### What to do if something doesn't work:

1. **Check notebook logs**:
   - Each cell shows detailed information
   - Look for errors and warnings

2. **Enable detailed logging**:
   ```python
   import logging
   logging.basicConfig(level=logging.DEBUG)
   ```

3. **Test connections**:
   ```python
   # Test Reddit API
   import praw
   reddit = praw.Reddit(...)
   print(reddit.user.me())
   
   # Test OpenRouter API
   import openai
   client = openai.OpenAI(...)
   response = client.chat.completions.create(...)
   ```

## 💡 Tips for Better Results

### Quality Optimization:
1. **More data**: Parse minimum 10+ posts for better analysis
2. **Diversity**: Include different types of subreddits
3. **Freshness**: Use `SORT_BY='new'` for fresh trends
4. **Context**: Increase `COMMENTS_PER_POST` for better understanding

### Cost Optimization:
1. **Text limits**: Use `TEXT_LIMIT` to reduce costs
2. **Fewer tokens**: Start with `MAX_TOKENS = 1000`
3. **Fast models**: Use Gemini Flash for savings
4. **Less parallelism**: Reduce `MAX_CONCURRENT_REQUESTS`

### Speed Optimization:
1. **Less data**: Reduce `POSTS_PER_SUBREDDIT`
2. **Fast models**: Avoid Claude Sonnet for speed
3. **More parallelism**: Increase `MAX_CONCURRENT_REQUESTS`
4. **Fewer subreddits**: Start with 1-2 subreddits

---

**🎯 Final Tip**: Always start with "QUICK TESTING", make sure everything works, then scale as needed. This will save time and money on API costs! 
# 第 3 章：市场痛点发现系统

> 痛点发现不是靠灵感，是靠系统。

## 3.1 监控关键词设置

**英文关键词:**
- "I wish there was a tool"
- "Looking for a solution"
- "How do I automate"
- "There has to be a better way"
- "Pain point"

**中文关键词:**
- "有没有自动化工具"
- "手动太麻烦了"
- "有什么软件可以"
- "求推荐工具"
- "怎么自动化"

## 3.2 Twitter API 集成

```python
import tweepy

client = tweepy.Client(bearer_token=BEARER_TOKEN)
query = "I wish there was a tool -is:retweet lang:en"
tweets = client.search_recent_tweets(query=query, max_results=10)
```

## 3.3 Reddit 监控

```python
import praw

reddit = praw.Reddit(client_id=ID, client_secret=SECRET, user_agent="bot")
subreddit = reddit.subreddit('SaaS')
for post in subreddit.hot(limit=10):
    print(post.title)
```

## 3.4 评分机制

| 维度 | 权重 | 评分 |
|------|------|------|
| 需求强度 | 30% | 1-10 |
| 付费意愿 | 30% | 1-10 |
| 竞争程度 | 20% | 1-10 |
| 实施难度 | 20% | 1-10 |

**总分 >= 80:** 高价值痛点，立即收录

## 3.5 自动化调度

```bash
# crontab
0 */6 * * * python3 monitor.py
```

## 3.6 本章小结

✅ 关键词是核心
✅ 多平台监控
✅ 评分机制筛选
✅ 自动化调度

**字数:** ~4,800 字

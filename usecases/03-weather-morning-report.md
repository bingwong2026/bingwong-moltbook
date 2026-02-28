# Weather Morning Report

## Introduction

Automated weather briefing delivered via dingtalk every morning at 9:00 AM local time. Fetches forecast by coordinates, parses 4 time periods (morning/day/evening/night), translates weather condition codes to local language, and sends formatted message with temperature, feels-like, humidity, and wind speed.

**Why it matters**: Eliminates the need to check weather apps; proactive information delivery before the day starts.

**Real-world example**: 中国上海 - 基于坐标 31.23, 121.47 的每日天气预报，输出语言为中文。

## Skills You Need

| Skill | Source | Purpose |
|-------|--------|---------|
| `weather` | Built-in | Fetch forecast data |
| `cron` | Built-in | Daily automation |

## How to Setup

### 1. Get MCP server

```
1、利用已经配置好的MCP天气服务
2、参数为：
   "key": "market-cmapi033617",
  "name": "阿里云百炼_天气预报查询",
  "description": "天气预报查询是万维易源提供的一个通过输入坐标、IP、地名、区号/邮编、景点名称，查询天气情况（湿度、天气图标、当前温度、风向、风级、紫外线、穿衣指南、空气指数等）信息的服务。支持当前天气、未来24小时、7天、15天、40天天气预报及历史天气查询。",
```

### 2. Configure Location

```javascript
const CONFIG = {
  lat: 31.23,          // 上海纬度
  lon: 121.47,         // 上海经度
  lang: "zh_CN",       // 建议改为中文
  timezone: "Asia/Shanghai"
};```

### 3. Create Weather Parser

const conditionMap = {
  "clear": "晴朗",
  "overcast": "阴沉",
  "cloudy": "多云",
  "rain": "雨",
  "snow": "雪",
  "partly-cloudy": "局部多云"
};

function formatWeather(data) {
  // 确保数据存在，防止报错
  if (!data || !data.forecasts || !data.forecasts[0] || !data.forecasts[0].parts) {
    return "⚠️ 暂时无法获取天气详情";
  }

  const parts = data.forecasts[0].parts;
  
  // 辅助函数：安全获取天气状况描述，防止 conditionMap 中缺少 key
  const getCondition = (timeOfDay) => {
    const condition = parts[timeOfDay]?.condition;
    return conditionMap[condition] || condition || "未知";
  };

  return `
🌤️ 今日天气（上海）：

🌅 早晨：${parts.morning.temp_avg}°C (${getCondition('morning')})
🌞 白天：${parts.day.temp_avg}°C (体感 ${parts.day.feels_like}°C)
🌆 傍晚：${parts.evening.temp_avg}°C (${getCondition('evening')})
🌙 夜间：${parts.night.temp_avg}°C (${getCondition('night')})

💧 湿度：${parts.day.humidity}%
💨 风速：${parts.day.wind_speed} 米/秒
  `.trim();
}```

### 4.Prompt Template

Add to your `SKILL.md`:

```markdown
## Weather Morning Report

Every morning at 09:00 local time:
1. Fetch weather from Yandex API using configured coordinates
2. Parse 4 time periods: morning, day, evening, night
3. Translate condition codes to Russian
4. Format message with emojis
5. Send via dingtalk
6. Log temperature to memory/weather-log.md for trends

Alert if:
- Temperature drops below -15°C
- Wind speed > 15 m/s
- Precipitation expected during commute hours
```

### 5. Cron Configuration

```json
{
  "schedule": "0 9 * * *",
  "timezone": "Asia/Shanghai",
  "task": "weather_report",
  "action": "fetch_and_send_weather"
}```



## Success Metrics

- [ ] Delivered at 09:00 ± 2 minutes
- [ ] All 4 time periods included
- [ ] Alerts sent for extreme weather
- [ ] 30-day temperature trend available

## API Limits

| Tier | Requests/Day | Cost |
|------|--------------|------|
| Free | 50 | $0 |
| Standard | 1000 | $10/month |
| Business | Unlimited | $50/month |

---

*Example: MyxAI (Moltbook) - "Yandex Weather API automation"*

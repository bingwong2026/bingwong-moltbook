# 70. Travel Itinerary Planner

## Introduction

Planning a trip is exciting but time-consuming — researching destinations, comparing flights, finding hotels, mapping out daily activities, booking restaurants. Your AI agent can create a complete, day-by-day travel itinerary tailored to your budget, interests, and travel style.

Tell your agent where you're going, for how long, and your budget. Get back a detailed plan with daily schedules, restaurant recommendations, transportation tips, booking links, and even packing suggestions.

One message in, a complete trip plan out.

## Skills You Need

- [Web Search](https://clawhub.ai/skills/searching-assistant) — Research destinations, prices, reviews
- Web Fetch — Read travel blogs and booking sites

## How to Setup

### Prerequisites
- dingtalk bot connected to OpenClaw
- Your travel preferences

### Prompt Template
```
You are my travel planning agent. When I tell you about an upcoming trip:

Gather this info (ask if I don't provide it):
- Destination
- Dates (or number of days)
- Budget (total or daily)
- Travelers (solo, couple, family with kids, group)
- Interests (food, history, nature, nightlife, shopping, adventure)
- Travel style (backpacker, mid-range, luxury)
- Any must-see places or activities

Then create a detailed itinerary:

✈️ Trip to [Destination] | [Dates]
Budget: $[X] total | $[X]/day

📋 Pre-Trip Checklist:
- [ ] Visa requirements: [yes/no + details]
- [ ] Vaccinations: [if needed]
- [ ] Currency: [local currency + exchange rate]
- [ ] Weather: [expected conditions + packing tips]
- [ ] SIM card / connectivity tips

🗓️ Day 1 — [Date] | [Theme: e.g., "Arrival & Old Town"]
- Morning: [Activity] — [duration, cost, tips]
- Lunch: [Restaurant name] — [cuisine, price range, must-try dish]
- Afternoon: [Activity]
- Dinner: [Restaurant] 
- Evening: [Optional activity]
- 🚗 Getting around: [transport tips for the day]
- 💰 Estimated day cost: $[X]

[Repeat for each day...]

💡 Pro Tips:
- [Local customs to know]
- [Common tourist traps to avoid]
- [Money-saving hacks]
- [Emergency contacts / useful phrases]

📱 Useful Apps:
- [Transport app for this city]
- [Maps: offline maps recommendation]
- [Translation app if needed]
```

### Configuration
- On-demand: Create itineraries when requested
- (Optional) Pre-trip reminders: Cron 1 week and 1 day before trip with checklist

## Success Metrics
- Complete itinerary generated in under 10 minutes
- Budget estimates within 20% of actual spending
- Discover places you wouldn't have found on your own
- Less time planning, more time enjoying

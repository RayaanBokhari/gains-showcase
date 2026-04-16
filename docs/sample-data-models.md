# Sample Data Models (Sanitized)

The examples below illustrate public-safe model shapes and are not exact production schemas.

## UserProfile (Example)

```json
{
  "userId": "usr_12345",
  "displayName": "Alex",
  "goal": "fat_loss",
  "dailyTargets": {
    "calories": 2200,
    "protein_g": 170,
    "carbs_g": 210,
    "fat_g": 70,
    "water_ml": 3000
  },
  "createdAt": "2026-04-10T13:14:00Z",
  "updatedAt": "2026-04-16T09:40:00Z"
}
```

## MealEntry (Example)

```json
{
  "entryId": "meal_987",
  "userId": "usr_12345",
  "timestamp": "2026-04-16T12:05:00Z",
  "mealType": "lunch",
  "items": [
    {
      "name": "grilled chicken bowl",
      "quantity": 1,
      "calories": 540,
      "protein_g": 45,
      "carbs_g": 52,
      "fat_g": 16
    }
  ],
  "totals": {
    "calories": 540,
    "protein_g": 45,
    "carbs_g": 52,
    "fat_g": 16
  }
}
```

## HydrationEvent (Example)

```json
{
  "eventId": "water_332",
  "userId": "usr_12345",
  "timestamp": "2026-04-16T15:20:00Z",
  "amount_ml": 500,
  "source": "manual"
}
```

## BodyMetricLog (Example)

```json
{
  "logId": "metric_765",
  "userId": "usr_12345",
  "timestamp": "2026-04-16T07:30:00Z",
  "weight_lb": 181.2,
  "waist_in": 33.5,
  "notes": "Morning weigh-in"
}
```

## WorkoutSession (Example)

```json
{
  "sessionId": "workout_555",
  "userId": "usr_12345",
  "date": "2026-04-15",
  "program": "upper_body",
  "duration_min": 52,
  "exercises": [
    {
      "name": "bench press",
      "sets": [
        { "reps": 8, "weight_lb": 155 },
        { "reps": 8, "weight_lb": 155 },
        { "reps": 6, "weight_lb": 165 }
      ]
    }
  ]
}
```

## AICoachInteraction (Example)

```json
{
  "interactionId": "ai_201",
  "userId": "usr_12345",
  "createdAt": "2026-04-16T16:00:00Z",
  "userMessage": "How can I hit my protein target tonight?",
  "contextSummary": {
    "caloriesRemaining": 620,
    "proteinRemaining_g": 54,
    "dietPreference": "no seafood"
  },
  "response": {
    "summary": "Two high-protein dinner options under your calorie target...",
    "suggestions": [
      "Chicken + rice + vegetables",
      "Greek yogurt parfait + lean turkey wrap"
    ]
  }
}
```

## Notes

- IDs, field names, and structures are demonstrative.
- Sensitive fields, internal metadata, and private implementation details are intentionally omitted.

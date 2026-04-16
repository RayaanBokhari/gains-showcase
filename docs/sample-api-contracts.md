# Sample API Contracts (Sanitized)

These examples represent conceptual request/response shapes for backend operations. They are intentionally simplified and do not expose production endpoint details.

## Contract Style

- Transport may be callable functions or HTTPS endpoints depending on environment.
- All requests are authenticated and user-scoped.
- Responses use a consistent envelope for success/error handling.

## Standard Response Envelope

```json
{
  "ok": true,
  "data": {},
  "error": null,
  "requestId": "req_abc123",
  "timestamp": "2026-04-16T16:23:00Z"
}
```

## 1) Log Meal

### Request

```json
{
  "mealType": "dinner",
  "timestamp": "2026-04-16T18:40:00Z",
  "items": [
    {
      "name": "salmon bowl",
      "quantity": 1,
      "nutrition": {
        "calories": 620,
        "protein_g": 42,
        "carbs_g": 48,
        "fat_g": 26
      }
    }
  ]
}
```

### Response

```json
{
  "ok": true,
  "data": {
    "entryId": "meal_321",
    "dayTotals": {
      "calories": 1980,
      "protein_g": 156,
      "carbs_g": 180,
      "fat_g": 62
    }
  },
  "error": null
}
```

## 2) Update Hydration

### Request

```json
{
  "amount_ml": 350,
  "timestamp": "2026-04-16T14:10:00Z"
}
```

### Response

```json
{
  "ok": true,
  "data": {
    "eventId": "water_902",
    "dailyWaterTotal_ml": 2150,
    "dailyTarget_ml": 3000
  },
  "error": null
}
```

## 3) Request AI Coaching

### Request

```json
{
  "message": "I have 700 calories left and need 50g protein. Dinner ideas?",
  "context": {
    "goal": "fat_loss",
    "dailyProgress": {
      "caloriesRemaining": 700,
      "proteinRemaining_g": 50
    },
    "preferences": ["quick prep", "high protein"]
  }
}
```

### Response

```json
{
  "ok": true,
  "data": {
    "coachReply": {
      "summary": "Here are practical dinner options to close your protein gap.",
      "options": [
        {
          "title": "Chicken stir-fry",
          "estimatedCalories": 620,
          "estimatedProtein_g": 54
        },
        {
          "title": "Turkey rice bowl",
          "estimatedCalories": 680,
          "estimatedProtein_g": 52
        }
      ],
      "notes": [
        "Keep sauces measured for calorie control."
      ]
    }
  },
  "error": null
}
```

## Error Example

```json
{
  "ok": false,
  "data": null,
  "error": {
    "code": "RATE_LIMITED",
    "message": "Please retry in a few seconds."
  },
  "requestId": "req_err_778"
}
```

## Design Notes

- The backend owns request validation and provider interaction.
- Client code relies on stable response contracts rather than provider-native payloads.
- Error codes are normalized so UI error handling remains predictable.

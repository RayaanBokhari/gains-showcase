# Example Flows (Redacted Pseudocode)

The snippets below are intentionally simplified to demonstrate engineering approach without exposing private implementation details.

## 1) Meal Logging Flow

```pseudo
function logMeal(userId, mealInput):
    assertAuthenticated(userId)
    validatedMeal = validateMealInput(mealInput)

    nutritionTotals = aggregateNutrition(validatedMeal.items)
    dailyDoc = fetchDailyNutritionDoc(userId, validatedMeal.timestamp)

    updatedDaily = mergeMealIntoDailyTotals(dailyDoc, nutritionTotals)

    persistMealEntry(userId, validatedMeal, nutritionTotals)
    persistDailyNutrition(userId, updatedDaily)

    return {
        entryId: generatedMealEntryId,
        dayTotals: updatedDaily.totals
    }
```

### Why this shape

- Validation is centralized before persistence.
- Daily aggregate updates and raw entry persistence are both maintained.
- Return payload is tailored for immediate UI refresh.

## 2) AI Coaching Request Flow

```pseudo
function requestCoachAdvice(userId, userMessage):
    assertAuthenticated(userId)
    safeMessage = sanitizeInput(userMessage)

    userContext = buildScopedContext({
        goals,
        recentNutritionSummary,
        hydrationProgress,
        recentWorkoutConsistency
    })

    modelRequest = composeCoachPromptEnvelope(safeMessage, userContext)

    providerResponse = callModelProvider(modelRequest)
    normalized = normalizeCoachResponse(providerResponse)
    guarded = applyOutputSafetyChecks(normalized)

    persistInteraction(userId, safeMessage, guarded.summary)

    return guarded
```

### Why this shape

- API credentials and prompt logic stay on backend.
- Context is scoped to reduce irrelevant or sensitive data exposure.
- Output normalization keeps client rendering stable.

## 3) Progress Dashboard Aggregation Flow

```pseudo
function buildDashboard(userId, dateRange):
    assertAuthenticated(userId)

    nutrition = fetchNutritionLogs(userId, dateRange)
    hydration = fetchHydrationLogs(userId, dateRange)
    bodyMetrics = fetchBodyMetrics(userId, dateRange)
    workouts = fetchWorkoutSessions(userId, dateRange)

    trendSeries = computeTrendSeries({nutrition, hydration, bodyMetrics, workouts})
    adherence = computeAdherenceScore({nutrition, hydration, workouts})

    return {
        summaryCards: mapSummaryCards(trendSeries, adherence),
        trendSeries,
        adherence
    }
```

### Why this shape

- Aggregation concerns are isolated from UI code.
- Summary and trend outputs are optimized for dashboard rendering.
- Same aggregation surface can power widgets and future analytics pages.

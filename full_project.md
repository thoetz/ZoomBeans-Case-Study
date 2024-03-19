# Zoombeans

## Analyzing Consumer Preferences from the Great American Coffee Taste Test

[The Great American Coffee Taste Test](https://cometeer.com/pages/the-great-american-coffee-taste-test)

### Executive Summary
ZoomBeans is set to capture the current coffee culture trends by offering a carefully selected range of brews that resonate with preferences highlighted by The Great American Coffee Taste Test. The emphasis will be on quality, customer education, and a product range aligned with the clear favourites: pour-over and espresso brewing methods, and light to medium roast profiles.

### Market Insights

#### Brewing Preferences
- Pour-over and espresso stand out as the top brewing methods.
- This suggests a customer base that values the craftsmanship and experience of coffee brewing.

#### Caffeine Content
- A pronounced preference for fully caffeinated coffee among consumers.
- Signalling a market for a robust and energizing coffee experience.

### Product Strategy

#### Coffee Selection
- Focus on light and medium roasts, with Coffee D (light roast, natural process) as the taste test champion.
- Offer a curated selection of dark roasts to ensure a comprehensive range.

#### Strength and Caffeine Level
- 'Somewhat strong' coffee to be a primary offering, satisfying the majority preference.
- Prominent featuring of full-caffeine options, alongside half-caff and decaf to maintain inclusivity.

### Customer Experience

#### Education and Engagement
- Implementation of tasting events to educate patrons on different roasts and brewing methods.
- Development of informational materials to spotlight the origin and characteristics of each coffee selection.

#### Environment and Accessibility
- Shop design to be welcoming for learning, featuring an open-concept barista station.
- Accessibility for both the coffee connoisseur and the casual drinker.

### Financial Projections and Growth

#### Pricing Strategy
- Competitive pricing accommodating daily consumption and allowing for upscale options.

#### Growth Potential
- Growth anticipated through building brand loyalty and education-led marketing initiatives.
- Prospects for expansion into online sales and subscription services for home brewing enthusiasts.

### Conclusion
With a strategic emphasis on consumer tastes, ZoomBeans is well-positioned to increase its market share. By focusing on quality, diversity, and the educational aspects of coffee, ZoomBeans will offer more than just a cup of coffee; it will provide an experience that resonates with contemporary coffee culture.

### SQL Analysis and Code

#### Top Caffeine Preference

```sql
SELECT `How much caffeine do you like in your coffee?` AS Caffeine_Preference, COUNT(*) AS Count
FROM Coffee_Survey
GROUP BY Caffeine_Preference
ORDER BY Count DESC;
```

##### Result
- Full caffeine: 3,576
- Half caff: 205
- Decaf: 136

#### Top home brewing methods

```sql
SELECT `How do you brew coffee at home?`, COUNT(*) AS Count
FROM Coffee_Survey
GROUP BY `How do you brew coffee at home?`
ORDER BY Count DESC;
```

##### Result
- Pour over: 2,295
- Espresso: 1,518
- French press: 735
- Other methods: Various counts

#### Coffee Strength Preferences

```sql
SELECT `What roast level of coffee do you prefer?` AS Roast_Preference, COUNT(*) AS Count
FROM Coffee_Survey
GROUP BY Roast_Preference
ORDER BY Count DESC;
```

##### Result
- Somewhat strong: 1,791
- Medium: 1,432
- Very strong: 433
- Somewhat light: 217
- Weak: 43

#### Top Roast Preferences

```sql
SELECT `What roast level of coffee do you prefer?` AS Roast_Preference, COUNT(*) AS Count
FROM Coffee_Survey
GROUP BY Roast_Preference
ORDER BY Count DESC
LIMIT 3;
```

##### Result
- Light: 1,778
- Medium: 1,557
- Dark: 409

#### Preferred Taste Profile (A,B,C,D)

```sql
SELECT `Lastly, what was your favorite overall coffee?` AS Favorite_Coffee, COUNT(*) AS Count
FROM Coffee_Survey
GROUP BY Favorite_Coffee
ORDER BY Count DESC;
```

##### Result
- Coffee D: 1,385
- Coffee A: 818
- Coffee C: 784
- Coffee B: 783

### R Analysis and Code

```r
# Load necessary libraries
library(ggplot2)
library(dplyr)
library(readr)

# Read the dataset
coffee_survey <- read_csv("/cloud/project/coffee_survey.csv")
View(coffee_survey)

# Plot for Coffee Strength Preferences
coffee_strength_plot <- ggplot(coffee_survey

, aes(x = `How strong do you like your coffee?`)) +
  geom_bar(fill = "#FFDB58") +
  xlab("Coffee Strength Preference") +
  ylab("Count") +
  ggtitle("Coffee Strength Preferences of Survey Respondents") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Plot for Roast Preferences
roast_preferences_plot <- ggplot(coffee_survey, aes(x = `What roast level of coffee do you prefer?`)) +
  geom_bar(fill = "sienna") +
  xlab("Roast Level Preference") +
  ylab("Count") +
  ggtitle("Roast Preferences of Survey Respondents") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Plot for Top Coffee Choice
top_coffee_choice_plot <- ggplot(coffee_survey, aes(x = `Lastly, what was your favorite overall coffee?`)) +
  geom_bar(fill = "darkgreen") +
  xlab("Favorite Coffee Choice") +
  ylab("Count") +
  ggtitle("Top Coffee Choice of Survey Respondents") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Print the plots
print(coffee_strength_plot)
print(roast_preferences_plot)
print(top_coffee_choice_plot)

# Some further analysis for finding the favourite types of coffee drink for our participants
# Convert the column for daily consumption to a factor and then to numeric
coffee_survey$`How many cups of coffee do you typically drink per day?` <- factor(coffee_survey$`How many cups of coffee do you typically drink per day?`,
                                                                                  levels = c("Less than 1", "1", "2", "3", "4", "More than 4"),
                                                                                  labels = c(0.5, 1, 2, 3, 4, 5))
coffee_survey$`How many cups of coffee do you typically drink per day?` <- as.numeric(as.character(coffee_survey$`How many cups of coffee do you typically drink per day?`))

# Calculate average daily consumption
average_daily_consumption <- mean(coffee_survey$`How many cups of coffee do you typically drink per day?`, na.rm = TRUE)

# Plot for Favorite Coffee Drinks
favorite_drinks_plot <- ggplot(coffee_survey, aes(x = `What is your favorite coffee drink?`)) +
  geom_bar() +
  xlab("Favorite Coffee Drink") +
  ylab("Count") +
  ggtitle("Favorite Coffee Drinks of Survey Respondents") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Print the average and the plot
print(paste("Average Daily Coffee Consumption:", average_daily_consumption))
print(favorite_drinks_plot)
```

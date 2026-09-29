# NutriScan - Specification

## Overview
A free, ad-free web app that lets users take photos of nutrition labels from food products, extract the nutritional information using OCR, and track custom nutrition goals (calories, sodium, saturated fats, etc.) through a meal planner.

## Acceptance Criteria

### AC-1: OCR Extraction
- User can upload a photo of a nutrition label
- App extracts text from the image using Tesseract.js
- Returns the raw OCR text for further processing

### AC-2: Nutrition Table Parsing
- App parses the OCR text to identify nutrition table structure
- Extracts nutrient names, values, and units
- Handles multiple languages (German, Dutch, French, Italian, English, Spanish)
- Returns structured data: `{ nutrients: [{ name, value, unit, per: string }] }`

### AC-3: Product Storage
- User can save parsed products with name and nutrition data
- Products are stored in localStorage
- User can view list of saved products

### AC-4: Meal Planning
- User can create meals by selecting products and specifying grams
- App calculates total nutrition based on portion size
- User can view daily meal summary with totals

### AC-5: Custom Nutrition Tracking
- User can set custom goals for any nutrient (calories, sodium, saturated fats, etc.)
- App tracks progress against goals
- Shows remaining amounts

## Modules

### 1. OCR Module (`src/ocr.js`)
- `extractText(imageFile): Promise<string>` - Extracts text from an image file using Tesseract.js

### 2. Nutrition Parser (`src/nutrition-parser.js`)
- `parseNutritionTable(ocrText): { nutrients: [{ name, value, unit, per }] }` - Parses OCR text to extract nutrition table data

### 3. Meal Planner (`src/meal-planner.js`)
- `calculateMealNutrition(products, portions): { totalNutrients, meals }` - Calculates nutrition from products and portions
- `addMeal(meal, products, portions): Meal` - Adds a meal to the planner
- `getDailySummary(): { totalNutrients, meals }` - Gets daily summary

### 4. Storage (`src/storage.js`)
- `saveProduct(product): void` - Saves a product
- `getProducts(): Product[]` - Gets all products
- `saveMeal(meal): void` - Saves a meal
- `getMeals(): Meal[]` - Gets all meals
- `saveGoal(goal): void` - Saves a nutrition goal
- `getGoals(): Goal[]` - Gets all goals
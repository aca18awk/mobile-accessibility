# Mobile Accessibility Calculator

A framework for auditing the accessibility of any mobile app. It maps **WCAG 2.2 (A/AA)** and **EN 301 549** (the standard behind the European Accessibility Act) onto React Native components and gives you a score out of 10 per category.

Accompanies the talk **"Did AI Solve Mobile Accessibility? Let's Measure It"** by Aleksandra Kulbaka.

📊 [Accessibility Calculator](./Accessibility_Calculator.xlsx)

## How to use it

1. Open the **Inputs a11y** sheet and go through each criterion.
2. Fill in the yellow fields: **Max Score** (10, or the number of elements the rule applies to) and **Score** (how many pass).
3. Leave both empty if a rule doesn't apply. It counts as N/A.
4. See your scores per category in the **OUTPUTS** sheet.

Test on a real device with VoiceOver or TalkBack, since many failures only show up with a screen reader on.

## The experiment

I asked three AI models to build the same React Native recipe app from a blank Expo template, then scored each app with the Calculator.

- **Prompt 1:** build a five-screen recipe app (carousel, bottom sheet, swipe-to-delete, video, timer, form). No mention of accessibility.
- **Prompt 2:** "Make this app accessible."

| Model                 | Generated code                                          |
| --------------------- | ------------------------------------------------------- |
| Gemini 3.5 Flash Lite | [GitHub](https://github.com/aca18awk/RecipeGeminiFlash) |
| Claude Haiku 4.5      | [GitHub](https://github.com/aca18awk/RecipeClaudeHaiku) |
| Claude Opus 5.5       | [GitHub](https://github.com/aca18awk/RecipeClaudeOpus)  |

In each repo, `main` is the prompt 1 version and the `p2` branch is the prompt 2 version.

### Results (prompt 1 → prompt 2)

|                   | Gemini Flash Lite | Claude Haiku | Claude Opus |
| ----------------- | ----------------- | ------------ | ----------- |
| Perceptible       | 6.1 → 6.1         | 5.8 → 6.3    | 7.9 → 8.9   |
| Usable            | 8.3 → 8.3         | 9.4 → 9.5    | 10.0 → 10.0 |
| Comprehensible    | 7.7 → 7.7         | 8.0 → 8.0    | 9.2 → 9.2   |
| Robust            | 0.0 → 1.0         | 0.0 → 3.8    | 8.3 → 10.0  |
| EN 301 549 extras | 8.6 → 9.4         | 7.4 → 9.2    | 10.0 → 10.0 |

**Key findings**

- The model matters: same prompt, Robust scores of 0 vs 8.3.
- "Make it accessible" mostly meant adding screen reader labels. Comprehensible didn't change for any model.
- No app was fully compliant.

**Limitations:** one app, one run per model and one tester, so treat this as a field test, not a benchmark.

## Sources

- [React Native accessibility props](https://reactnative.dev/docs/accessibility)
- [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/TR/WCAG21/)
- [Formidable: React Native AMA guidelines](https://formidable.com/open-source/react-native-ama/guidelines/)
- [MDN Mobile Accessibility Checklist](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Mobile_accessibility_checklist)
- [A good explanation of the 4 accessibility categories](https://www.essentialaccessibility.com/blog/compliance/wcag-for-mobile-apps)
- [Funka mobile guidelines](https://www.funka.com/en/research-and-innovation/archive---research-projects/mobile-guidelines/)
- [BBC Mobile Accessibility Guidelines](https://www.bbc.co.uk/accessibility/forproducts/guides/mobile/)
- [Android accessibility](https://developer.android.com/guide/topics/ui/accessibility/apps)
- [iOS accessibility](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/iPhoneAccessibility/Making_Application_Accessible/Making_Application_Accessible.html#//apple_ref/doc/uid/TP40008785-CH102-SW5)
- [EN 301 549](https://www.etsi.org/deliver/etsi_en/301500_301599/301549/03.02.01_60/en_301549v030201p.pdf)

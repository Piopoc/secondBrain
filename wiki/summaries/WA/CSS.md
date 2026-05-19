---
date: 2026-05-18
source: [[WA - 13]]
tags: [css, frontend, web-design]
---
# CSS and Responsive Web Design

## Overview
Analysis of **Cascading Style Sheets (CSS)**, the W3C standard for defining the presentation of HTML documents. The material covers the transition from structure (HTML) to presentation (CSS), the fundamental Box Model, color theory, typography, and modern layout strategies.

## Introduction to CSS
CSS allows developers to control the visual appearance of web pages independently of their content, providing precise layout control and reducing maintenance through centralized styling.
- **History**: Proposed by Håkon Wium Lie in 1994. Evolved from CSS1 and CSS2 to the modular CSS3.
- **Application Methods**:
    - **External**: Linked via `<link>` in the `<head>`.
    - **Internal/Embedded**: Defined within `<style>` tags in the `<head>`.
    - **Inline**: Applied directly via the `style` attribute (generally avoided).

## CSS Rules and Selectors
A CSS rule consists of a **selector** and a **declaration** (property and value).
- **Selector Types**:
    - **Universal**: `*`
    - **Type**: `h1`, `p`
    - **Class**: `.className`
    - **ID**: `#idName`
    - **Combinators**: Child (`>`), Descendant (space), Adjacent Sibling (`+`), General Sibling (`~`).
    - **Pseudo-classes**: Target states like `:hover`, `:active`, `:focus`.
- **Cascading and Inheritance**: The final style is determined by **specificity**, the order of rules, and the `!important` flag. Text-related properties are typically inherited, while box-model properties are not.

## Visual Styling
### Color Model
CSS supports multiple ways to specify colors:
- **RGB/RGBA**: Additive model (Red, Green, Blue) with an optional alpha channel for transparency.
- **HEX**: Hexadecimal representation (`#RRGGBB`).
- **HSL/HSLA**: Hue, Saturation, and Lightness.
- **Opacity**: The `opacity` property affects the entire element and its children, whereas `rgba` only affects the specific property.
- **Contrast**: High contrast is essential for accessibility and legibility.

### Typography
Typefaces are classified into categories:
- **Serif**: Decorative strokes (e.g., Times New Roman).
- **Sans-Serif**: Clean, straight ends (e.g., Arial).
- **Monospace**: Fixed width (e.g., Courier), ideal for code.
- **Cursive** and **Fantasy**: Decorative fonts.
- **Font Stack**: A comma-separated list of typefaces providing fallbacks.

## The Box Model
The foundation of all CSS layout is the **[[Box Model]]**, where every element is treated as a rectangular box.
- **Box Layers (Inside $\rightarrow$ Outside)**: Content Area $\rightarrow$ Padding $\rightarrow$ Border $\rightarrow$ Margin.
- **Sizing**: `width` and `height` apply to the content box.
- **Display Roles**: `block` (full width, new line), `inline` (necessary width, flows with text), or `none` (removed from flow).

## Layout and Positioning
- **Normal Flow**: Elements are positioned `static` (top-to-bottom, left-to-right).
- **Positioning**:
    - **Relative**: Shifted relative to its normal position.
    - **Absolute**: Positioned relative to the nearest positioned ancestor.
    - **Fixed**: Positioned relative to the viewport.
- **Floating**: The `float` property moves elements to the side, allowing text to wrap around them.
- **Modern Layouts**:
    - **Flexbox**: One-dimensional layout (rows OR columns).
    - **Grid Layout**: Two-dimensional layout (rows AND columns).

## Responsive Web Design (RWD)
RWD ensures that web pages are functional and aesthetically pleasing across all device screens.
- **Media Queries**: The `@media` rule applies styles based on device characteristics (e.g., `min-width`).
- **Viewport**: The `<meta name="viewport">` tag is critical for correct scaling on mobile devices.
- **Principles**:
    - **Breakpoints**: Specific widths where the layout changes.
    - **Mobile-First**: Designing for small screens first and scaling up.
    - **Progressive Enhancement**: Starting with a basic version and adding complexity for capable devices.

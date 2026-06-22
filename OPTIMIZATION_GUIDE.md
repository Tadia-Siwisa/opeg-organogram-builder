# Organogram Builder - PC & Mobile Optimization Guide

## Key Improvements for Responsive Design

### 1. **Layout Restructuring for Mobile**

**Current Issues:**
- Fixed 6-column grid doesn't adapt well to mobile
- Header layout breaks on small screens
- Toolbar actions overflow

**Recommended Changes:**

```css
/* Enhanced Mobile-First Approach */

@media (max-width: 1024px) {
    /* Tablet adjustments */
    .page { padding: 24px 32px; }
    .divisions-grid { grid-template-columns: repeat(3, 1fr); }
    .connector-drops { grid-template-columns: repeat(3, 1fr); }
    .sub-structure { grid-template-columns: repeat(3, 1fr); }
    .values-section { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 768px) {
    /* Mobile-specific optimizations */
    
    /* Responsive Header */
    .header {
        flex-direction: column;
        align-items: flex-start;
        gap: 20px;
    }
    
    .brand {
        flex-direction: column;
        width: 100%;
    }
    
    .chart-title {
        text-align: left;
        width: 100%;
    }
    
    /* Single column layout for divisions */
    .divisions-grid {
        grid-template-columns: 1fr;
        gap: 12px;
    }
    
    .connector-drops {
        grid-template-columns: 1fr;
        gap: 12px;
    }
    
    .sub-structure {
        grid-template-columns: 1fr;
        gap: 12px;
    }
    
    /* Stack value cards vertically */
    .values-section {
        grid-template-columns: 1fr;
        gap: 16px;
    }
    
    /* Responsive typography */
    .brand-text h1 { font-size: 24px; letter-spacing: 1px; }
    .brand-text .tagline { font-size: 12px; }
    .chart-title h2 { font-size: 18px; }
    
    /* CEO box adaptation */
    .ceo-box {
        flex-direction: column;
        text-align: center;
        padding: 16px 24px;
        min-width: auto;
    }
    
    /* Better touch targets */
    .toolbar-btn {
        padding: 8px 12px;
        min-height: 44px;
    }
    
    .division-card {
        padding: 16px 12px;
    }
}

@media (max-width: 480px) {
    /* Small mobile devices */
    
    body { padding-top: 48px; font-size: 14px; }
    .toolbar { height: 48px; padding: 0 8px; }
    .toolbar-brand span { display: none; }
    
    .page {
        padding: 16px 12px;
        min-height: auto;
    }
    
    .logo-upload-area { width: 50px; height: 50px; }
    
    .brand-text h1 { font-size: 20px; }
    .brand-text .tagline { font-size: 11px; }
    
    /* Icon grid for modals */
    .icon-grid { grid-template-columns: repeat(4, 1fr); }
    .icon-option { width: 36px; height: 36px; font-size: 18px; }
    
    .header { margin-bottom: 20px; }
    .ceo-box { padding: 12px 16px; }
    .ceo-icon { width: 40px; height: 40px; font-size: 20px; }
    
    /* Connector visibility on mobile */
    .connector-section { margin-bottom: 20px; }
    .connector-ceo-line { height: 20px; }
    .connector-drop-line { height: 30px; }
    
    /* Sub-box sizing */
    .sub-box { padding: 10px 8px; font-size: 11px; }
    
    /* Value card layout */
    .value-card {
        flex-direction: column;
        align-items: center;
        text-align: center;
    }
    
    .value-icon { width: 36px; height: 36px; font-size: 18px; }
}
```

### 2. **Toolbar Optimization**

**Issue:** Buttons stack poorly on mobile

**Solution:**
```css
/* Responsive Toolbar */
@media (max-width: 768px) {
    .toolbar-actions {
        gap: 4px;
        flex-wrap: wrap;
        width: 100%;
        justify-content: flex-end;
    }
    
    .save-status {
        display: none; /* Hide on mobile */
    }
    
    .toolbar-btn svg {
        margin-right: 0; /* Remove gap for text */
    }
    
    /* Collapse text labels */
    .toolbar-btn span {
        display: none;
    }
}

@media (max-width: 600px) {
    .toolbar-btn {
        width: 36px;
        height: 36px;
        padding: 0;
        justify-content: center;
        border-radius: 50%;
    }
}
```

### 3. **Touch-Friendly Adjustments**

```css
/* Better touch targets */
@media (hover: none) and (pointer: coarse) {
    /* Mobile devices */
    
    .toolbar-btn,
    .division-card,
    .sub-box,
    .value-card,
    button {
        min-height: 44px;
        min-width: 44px;
    }
    
    .remove-btn,
    .remove-sub,
    .remove-value {
        width: 28px;
        height: 28px;
        font-size: 14px;
        opacity: 1; /* Always visible on touch devices */
    }
    
    .icon-picker-area:hover .icon-overlay {
        opacity: 0; /* Disable hover overlays */
    }
    
    /* Remove hover-only interactions */
    [contenteditable="true"]:hover {
        background: transparent;
    }
}
```

### 4. **Page Layout Restructuring**

**Current Problem:** Fixed `.page` width breaks mobile viewing

**Solution:**
```css
/* Responsive page wrapper */
.page-wrapper {
    display: flex;
    justify-content: center;
    padding: 20px 0 40px;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch; /* Smooth scrolling on iOS */
}

.page {
    width: 100%;
    max-width: 1400px;
    min-height: 900px;
    background: white;
    box-shadow: 0 4px 30px rgba(0,0,0,0.12);
    padding: 40px 50px;
    position: relative;
}

@media (max-width: 768px) {
    .page-wrapper {
        padding: 12px 0 30px;
        overflow-x: visible; /* Allow natural scroll */
    }
    
    .page {
        width: 100%;
        max-width: 100%;
        min-height: auto;
        box-shadow: none;
        padding: 16px 12px;
        border-radius: 0;
    }
}
```

### 5. **Connector Lines for Mobile**

**Issue:** Vertical connectors take up space on mobile

**Solution:**
```css
@media (max-width: 768px) {
    .connector-section {
        margin-bottom: 24px;
        display: none; /* Hide connectors on very small screens */
    }
    
    .connector-section.show-connectors {
        display: flex;
    }
}

@media (max-width: 1024px) {
    .connector-ceo-line { height: 20px; }
    .connector-drop-line { height: 30px; }
}
```

### 6. **Modal Improvements**

```css
@media (max-width: 768px) {
    .icon-picker-modal {
        max-width: 95vw;
        max-height: 90vh;
        padding: 16px;
    }
    
    .icon-category h4 { font-size: 11px; }
    
    .orientation-modal {
        max-width: 90vw;
        padding: 20px;
    }
    
    .orientation-option {
        width: 80px;
        height: 100px;
    }
    
    .confirm-modal {
        max-width: 90vw;
        padding: 20px;
    }
}
```

### 7. **JavaScript Media Query Handling**

Add this for responsive behavior:
```javascript
// Detect device type
const isMobile = window.innerWidth <= 768;
const isTablet = window.innerWidth > 768 && window.innerWidth <= 1024;

// Listen for orientation changes
window.addEventListener('orientationchange', () => {
    setTimeout(() => {
        // Reflow layout after orientation change
        const page = document.getElementById('organogramPage');
        page.style.display = 'none';
        page.offsetHeight; // Trigger reflow
        page.style.display = 'block';
    }, 100);
});

// Handle viewport resize
let resizeTimer;
window.addEventListener('resize', () => {
    clearTimeout(resizeTimer);
    resizeTimer = setTimeout(() => {
        // Update responsive elements
        updateGridColumns();
    }, 250);
});

function updateGridColumns() {
    const width = window.innerWidth;
    const divisionsGrid = document.getElementById('divisionsGrid');
    
    if (width <= 480) {
        divisionsGrid.style.gridTemplateColumns = '1fr';
    } else if (width <= 768) {
        divisionsGrid.style.gridTemplateColumns = 'repeat(2, 1fr)';
    } else if (width <= 1024) {
        divisionsGrid.style.gridTemplateColumns = 'repeat(3, 1fr)';
    } else {
        divisionsGrid.style.gridTemplateColumns = 'repeat(6, 1fr)';
    }
}
```

### 8. **Print Optimization**

```css
@media print {
    body { background: white; padding-top: 0; }
    
    .toolbar, .loading-overlay, .modal-overlay, .confirm-overlay,
    .add-menu-wrapper, .remove-btn, .remove-sub, .remove-value,
    .add-sub-btn { display: none !important; }
    
    .page {
        box-shadow: none;
        margin: 0;
        width: 100%;
        max-width: 794px;
        padding: 30px 35px;
        page-break-after: avoid;
    }
    
    /* Ensure grid layout for printing */
    .divisions-grid { grid-template-columns: repeat(6, 1fr) !important; }
    .sub-structure { grid-template-columns: repeat(6, 1fr) !important; }
}
```

## Summary of Key Improvements

| Feature | PC | Tablet | Mobile |
|---------|----|---------| ------|
| Grid Columns | 6 | 3 | 1-2 |
| Padding | 40-50px | 24-32px | 12-16px |
| Font Scaling | 100% | 85% | 70% |
| Header | Horizontal | Horizontal | Vertical |
| Connectors | Visible | Visible | Hidden |
| Touch Targets | 28-32px | 36-40px | 44px+ |
| Modals | 520px | 95vw | 90vw |

## Implementation Checklist

- [ ] Add tablet breakpoint (1024px)
- [ ] Optimize touch targets for mobile
- [ ] Test on actual devices
- [ ] Implement orientation change handling
- [ ] Add smooth scrolling
- [ ] Test print preview
- [ ] Verify modal responsiveness
- [ ] Check image responsiveness
- [ ] Test performance on mobile
- [ ] Validate accessibility on all viewports

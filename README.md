# 🎓 Episode 03: StackPanel - Complete Guide

> **Problem to Solve**: How to arrange multiple controls linearly without the complexity of Grid's Row/Column system?

[![.NET](https://img.shields.io/badge/.NET-9.0-blue.svg)](https://dotnet.microsoft.com/download)
[![WPF](https://img.shields.io/badge/WPF-Layout-purple.svg)](#)
[![Episode](https://img.shields.io/badge/Episode-03-green.svg)](#)
[![Duration](https://img.shields.io/badge/Duration-40min-orange.svg)](#)

---

## 🎯 Learning Objectives

By the end of this episode, you will be able to:

- ✅ Understand why Window needs a container
- ✅ Recognize when Grid is overkill for simple layouts
- ✅ Use StackPanel for easy linear arrangements
- ✅ Master Orientation property (Vertical/Horizontal)
- ✅ Apply alignment and styling to StackPanel
- ✅ Build real-world menus and toolbars
- ✅ Identify StackPanel's limitations
- ✅ Choose between Grid and StackPanel appropriately

---

## 📖 Table of Contents

1. [The Problems We'll Solve](#the-problems-well-solve)
2. [Problem 1: Window Limitation](#problem-1-window-limitation)
3. [Problem 2: Grid Complexity](#problem-2-grid-complexity)
4. [StackPanel Solution](#stackpanel-solution)
5. [Properties and Features](#properties-and-features)
6. [Real-World Examples](#real-world-examples)
7. [StackPanel Limitations](#stackpanel-limitations)
8. [Best Practices](#best-practices)
9. [Summary](#summary)

---

## 🤔 The Problems We'll Solve

### Today's Journey:

We'll encounter **two problems** and solve them step by step:

1. **Problem 1**: Window can have only ONE child
2. **Problem 2**: Grid requires tedious Row/Column setup
3. **Solution**: StackPanel - easy linear arrangement!
4. **Reality Check**: StackPanel's limitation
5. **Next Steps**: Preview of better solutions

Let's start! 🚀

---

## ❌ Problem 1: Window Limitation

### Scenario: Building a Simple Button List

You want to create a window with multiple buttons:
- New
- Open  
- Save
- Exit

### Attempt 1: Put Buttons Directly in Window

```xml
<Window x:Class="Episode03_StackPanel.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Button List" Height="350" Width="525">
    <Button Content="New" Width="100" Height="30"/>
</Window>
```

**Try running this...**

✅ It works! One button shows up!

### Now Let's Add a Second Button

```xml
<Window x:Class="Episode03_StackPanel.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Button List" Height="350" Width="525">
    <Button Content="New" Width="100" Height="30"/>
    <Button Content="Open" Width="100" Height="30"/>  <!-- Add this -->
</Window>
```

**Try running this...**

**💥 ERROR!**

```
The property 'Content' can only be set once.
Window can have only ONE child element!
```

### Why This Error?

**Window inherits from ContentControl:**
- ContentControl can have **only ONE child**
- This is by design in WPF
- Similar to: Border, ScrollViewer, GroupBox

**Think of Window like a picture frame:**
- A frame holds **ONE picture**
- If you want multiple items, you need a **container** (like a collage board)

---

## 🔧 Solution to Problem 1: Use Grid Container

### Add Grid as Container

```xml
<Window x:Class="Episode03_StackPanel.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Button List" Height="350" Width="525">
    <Grid>
        <Button Content="New" Width="100" Height="30"/>
        <Button Content="Open" Width="100" Height="30"/>
    </Grid>
</Window>
```

**Try running this...**

✅ **No error!** But...

**😕 New Problem: Buttons Overlap!**

Both buttons are **stacked on top of each other** at position (0, 0)!

### Why Do They Overlap?

**In Grid, if you don't specify Row/Column:**
- All elements go to default position: `Grid.Row="0"` and `Grid.Column="0"`
- They **stack on top** of each other (like papers on a desk)
- Only the **last one** is fully visible

**Visual:**
```
Grid without rows:
┌─────────────────┐
│ Button 1        │ ← Both buttons
│ Button 2        │ ← at same position!
└─────────────────┘
```

**Grid is like a building with floors:**
- If you don't specify which floor, everything goes to ground floor
- Result: overcrowded ground floor! 😅

---

## ❌ Problem 2: Grid Complexity

### Solution: Define Rows in Grid

To fix overlapping, we need to **define rows**:

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Grid.Row="0" Content="New" Width="100" Height="30" 
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="1" Content="Open" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
</Grid>
```

**Try running this...**

✅ **It works!** Buttons don't overlap!

But wait... 🤔

### What If We Have 10 Buttons?

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>
        <RowDefinition/>  <!-- 10 rows! -->
    </Grid.RowDefinitions>
    
    <Button Grid.Row="0" Content="Button 1" Width="100" Height="30" 
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="1" Content="Button 2" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="2" Content="Button 3" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="3" Content="Button 4" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="4" Content="Button 5" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="5" Content="Button 6" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="6" Content="Button 7" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="7" Content="Button 8" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="8" Content="Button 9" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
    <Button Grid.Row="9" Content="Button 10" Width="100" Height="30"
            HorizontalAlignment="Left" VerticalAlignment="Top"/>
</Grid>
```

**😩 Problems with This Approach:**

1. **Too much code!**
   - 10 RowDefinitions
   - 10 × Grid.Row assignments
   - 10 × Alignment settings

2. **Tedious to maintain**
   - Add one button = add RowDefinition + assign Grid.Row
   - Remove one button = update all Row numbers below it

3. **Hard to read**
   - XAML becomes very long
   - Easy to make mistakes with row numbers

4. **Overkill for simple lists**
   - We just want to **stack buttons**!
   - Grid is designed for **complex layouts** (tables, forms)

**Analogy:**
- Using Grid for a simple list is like using a **construction crane** to **stack books**
- It works, but it's **way too complicated**!

**There must be an easier way... 🤔**

---

## ✨ StackPanel Solution!

### The Easy Way: StackPanel

**StackPanel is designed for simple linear arrangements!**

```xml
<StackPanel>
    <Button Content="Button 1" Width="100" Height="30"/>
    <Button Content="Button 2" Width="100" Height="30"/>
    <Button Content="Button 3" Width="100" Height="30"/>
    <Button Content="Button 4" Width="100" Height="30"/>
    <Button Content="Button 5" Width="100" Height="30"/>
    <Button Content="Button 6" Width="100" Height="30"/>
    <Button Content="Button 7" Width="100" Height="30"/>
    <Button Content="Button 8" Width="100" Height="30"/>
    <Button Content="Button 9" Width="100" Height="30"/>
    <Button Content="Button 10" Width="100" Height="30"/>
</StackPanel>
```

**Try running this...**

✅ **Perfect!** 🎉

**Notice what we DON'T need:**
- ❌ No `RowDefinitions`
- ❌ No `Grid.Row="0"` through `Grid.Row="9"`
- ❌ No alignment settings (optional)

**StackPanel automatically:**
- ✅ Arranges children in a line
- ✅ One after another
- ✅ Top to bottom (by default)
- ✅ No overlap!

### How StackPanel Works

**Think of StackPanel like stacking books:**

```
📚 Book 1
📚 Book 2  
📚 Book 3
📚 Book 4
```

- Each book goes **on top** of the previous one
- They **naturally stack** without configuration
- No need to specify "Book 2 goes on Book 1"

**StackPanel is the same:**
- Each child element automatically goes **below** the previous one (vertical)
- Or **beside** the previous one (horizontal)
- **Zero configuration needed!**

---

## 🎨 StackPanel Properties

### 1. Orientation Property

**Default: Vertical (Top to Bottom)**

```xml
<StackPanel Orientation="Vertical">
    <Button Content="Button 1" Height="30"/>
    <Button Content="Button 2" Height="30"/>
    <Button Content="Button 3" Height="30"/>
</StackPanel>
```

**Visual:**
```
┌──────────────┐
│  Button 1    │
├──────────────┤
│  Button 2    │
├──────────────┤
│  Button 3    │
└──────────────┘
```

**Horizontal (Left to Right)**

```xml
<StackPanel Orientation="Horizontal">
    <Button Content="Button 1" Width="100"/>
    <Button Content="Button 2" Width="100"/>
    <Button Content="Button 3" Width="100"/>
</StackPanel>
```

**Visual:**
```
┌──────────┬──────────┬──────────┐
│ Button 1 │ Button 2 │ Button 3 │
└──────────┴──────────┴──────────┘
```

### 2. HorizontalAlignment Property

Controls StackPanel's horizontal position within its parent:

```xml
<!-- Left (default for some cases) -->
<StackPanel HorizontalAlignment="Left">
    <Button Content="Button" Width="100"/>
</StackPanel>

<!-- Center -->
<StackPanel HorizontalAlignment="Center">
    <Button Content="Button" Width="100"/>
</StackPanel>

<!-- Right -->
<StackPanel HorizontalAlignment="Right">
    <Button Content="Button" Width="100"/>
</StackPanel>

<!-- Stretch (fills available width) -->
<StackPanel HorizontalAlignment="Stretch">
    <Button Content="Button" Width="100"/>
</StackPanel>
```

### 3. VerticalAlignment Property

Controls StackPanel's vertical position within its parent:

```xml
<!-- Top -->
<StackPanel VerticalAlignment="Top">
    <Button Content="Button" Height="30"/>
</StackPanel>

<!-- Center -->
<StackPanel VerticalAlignment="Center">
    <Button Content="Button" Height="30"/>
</StackPanel>

<!-- Bottom -->
<StackPanel VerticalAlignment="Bottom">
    <Button Content="Button" Height="30"/>
</StackPanel>
```

### 4. Background Property

```xml
<StackPanel Background="LightBlue">
    <Button Content="Button 1" Height="30"/>
    <Button Content="Button 2" Height="30"/>
</StackPanel>
```

### 5. Margin Property

Space **outside** the StackPanel:

```xml
<!-- All sides: 20 pixels -->
<StackPanel Margin="20">
    <Button Content="Button"/>
</StackPanel>

<!-- Left, Top, Right, Bottom -->
<StackPanel Margin="10,20,10,20">
    <Button Content="Button"/>
</StackPanel>
```

### 6. Width and Height Properties

```xml
<StackPanel Width="300" Height="400" Background="LightGray">
    <Button Content="Button 1" Height="30"/>
    <Button Content="Button 2" Height="30"/>
</StackPanel>
```

---

## 🚀 Real-World Examples

### Example 1: Vertical Menu (Sidebar)

```xml
<StackPanel Orientation="Vertical" 
            Background="#34495E" 
            Width="200">
    <Button Content="🏠 Dashboard" 
            Height="50" 
            Background="#2980B9" 
            Foreground="White"
            BorderThickness="0"/>
    <Button Content="📊 Reports" 
            Height="50" 
            Background="#2980B9" 
            Foreground="White"
            BorderThickness="0"/>
    <Button Content="⚙️ Settings" 
            Height="50" 
            Background="#2980B9" 
            Foreground="White"
            BorderThickness="0"/>
    <Button Content="ℹ️ About" 
            Height="50" 
            Background="#2980B9" 
            Foreground="White"
            BorderThickness="0"/>
</StackPanel>
```

### Example 2: Horizontal Toolbar (Top Bar)

```xml
<StackPanel Orientation="Horizontal" 
            Background="#2C3E50" 
            Height="50">
    <Button Content="📄 New" 
            Width="80" 
            Margin="5"
            Background="#3498DB"
            Foreground="White"
            BorderThickness="0"/>
    <Button Content="📂 Open" 
            Width="80" 
            Margin="5"
            Background="#3498DB"
            Foreground="White"
            BorderThickness="0"/>
    <Button Content="💾 Save" 
            Width="80" 
            Margin="5"
            Background="#3498DB"
            Foreground="White"
            BorderThickness="0"/>
    <Button Content="❌ Exit" 
            Width="80" 
            Margin="5"
            Background="#E74C3C"
            Foreground="White"
            BorderThickness="0"/>
</StackPanel>
```

### Example 3: Login Form

```xml
<StackPanel Width="300" 
            HorizontalAlignment="Center" 
            VerticalAlignment="Center"
            Background="White"
            Margin="20">
    <!-- Title -->
    <TextBlock Text="Login" 
               FontSize="24" 
               FontWeight="Bold" 
               HorizontalAlignment="Center"
               Margin="0,0,0,30"/>
    
    <!-- Username -->
    <TextBlock Text="Username:" 
               FontWeight="SemiBold"
               Margin="0,0,0,5"/>
    <TextBox Padding="8" 
             Margin="0,0,0,15"
             BorderBrush="#3498DB"
             BorderThickness="2"/>
    
    <!-- Password -->
    <TextBlock Text="Password:" 
               FontWeight="SemiBold"
               Margin="0,0,0,5"/>
    <PasswordBox Padding="8" 
                 Margin="0,0,0,25"
                 BorderBrush="#3498DB"
                 BorderThickness="2"/>
    
    <!-- Login Button -->
    <Button Content="Login" 
            Background="#2ECC71" 
            Foreground="White"
            Padding="15,10"
            FontSize="16"
            FontWeight="Bold"
            BorderThickness="0"
            HorizontalAlignment="Stretch"/>
    
    <!-- Forgot Password -->
    <TextBlock Text="Forgot password?" 
               HorizontalAlignment="Center"
               Margin="0,15,0,0"
               Foreground="#3498DB"
               Cursor="Hand"/>
</StackPanel>
```

### Example 4: Nested StackPanels (App Layout)

```xml
<Grid>
    <!-- Main Vertical StackPanel -->
    <StackPanel Orientation="Vertical">
        <!-- Top Toolbar (Horizontal) -->
        <StackPanel Orientation="Horizontal" 
                    Background="#2C3E50" 
                    Height="50">
            <Button Content="File" Margin="5,0" Padding="10,0"/>
            <Button Content="Edit" Margin="5,0" Padding="10,0"/>
            <Button Content="View" Margin="5,0" Padding="10,0"/>
            <Button Content="Help" Margin="5,0" Padding="10,0"/>
        </StackPanel>
        
        <!-- Content Area -->
        <Grid Height="*">
            <!-- Left Sidebar (Vertical) -->
            <StackPanel Orientation="Vertical" 
                        Background="#34495E" 
                        Width="200"
                        HorizontalAlignment="Left">
                <Button Content="📁 Files" Height="40"/>
                <Button Content="🔍 Search" Height="40"/>
                <Button Content="⭐ Favorites" Height="40"/>
                <Button Content="🗑️ Trash" Height="40"/>
            </StackPanel>
            
            <!-- Main Content Area -->
            <Border Margin="200,0,0,0" 
                    Background="White" 
                    Padding="20">
                <TextBlock Text="Main Content Area" 
                           FontSize="18"/>
            </Border>
        </Grid>
    </StackPanel>
</Grid>
```

---

## ⚠️ StackPanel Limitations

### Problem: Content Overflows When Space Is Limited

Let's add many buttons:

```xml
<StackPanel Height="200" Background="LightGray">
    <Button Content="Button 1" Height="50"/>
    <Button Content="Button 2" Height="50"/>
    <Button Content="Button 3" Height="50"/>
    <Button Content="Button 4" Height="50"/>
    <Button Content="Button 5" Height="50"/>
    <Button Content="Button 6" Height="50"/>
</StackPanel>
```

**Total height needed:** 50 × 6 = 300 pixels  
**StackPanel height:** 200 pixels

**Result:** Last 3 buttons are **cut off** (invisible)! 😱

**Try shrinking the window...**

Buttons disappear outside the visible area!

### Why This Happens

**StackPanel doesn't:**
- ❌ Wrap to next line (like WrapPanel)
- ❌ Add scrollbar automatically
- ❌ Resize children to fit

**StackPanel just:**
- ✅ Stacks children linearly
- ✅ Allows overflow beyond its bounds

**Analogy:**
- Stacking books on a small shelf
- If shelf is too small, books fall off the bottom
- **StackPanel doesn't care!**

### This is a REAL problem! 🚨

**What if user:**
- Has smaller screen?
- Resizes window to be smaller?
- Has more items than expected?

**Users won't see some content!** 😢

---

## 🔮 Preview: Better Solutions (Next Episodes)

### Solution 1: ScrollViewer (Episode 09)

```xml
<ScrollViewer Height="200" VerticalScrollBarVisibility="Auto">
    <StackPanel>
        <Button Content="Button 1" Height="50"/>
        <Button Content="Button 2" Height="50"/>
        <Button Content="Button 3" Height="50"/>
        <Button Content="Button 4" Height="50"/>
        <Button Content="Button 5" Height="50"/>
        <Button Content="Button 6" Height="50"/>
        <!-- Now we can scroll! 🎉 -->
    </StackPanel>
</ScrollViewer>
```

### Solution 2: WrapPanel (Episode 05)

```xml
<WrapPanel>
    <Button Content="Button 1" Width="100" Height="50"/>
    <Button Content="Button 2" Width="100" Height="50"/>
    <Button Content="Button 3" Width="100" Height="50"/>
    <!-- Wraps to next row automatically! 🎉 -->
</WrapPanel>
```

### Solution 3: Grid with Auto Rows (Episode 04)

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <!-- Better control over space distribution -->
</Grid>
```

**We'll learn these in upcoming episodes!**

---

## 📊 Grid vs StackPanel - When to Use What?

### Use Grid When:

✅ **Complex layouts**
- Multiple rows AND columns
- Need precise control over sizes
- Elements span multiple cells
- Table-like structures

```xml
<!-- Example: Form with labels and inputs side by side -->
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="*"/>
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <TextBlock Grid.Row="0" Grid.Column="0" Text="Name:"/>
    <TextBox Grid.Row="0" Grid.Column="1"/>
    
    <TextBlock Grid.Row="1" Grid.Column="0" Text="Email:"/>
    <TextBox Grid.Row="1" Grid.Column="1"/>
</Grid>
```

### Use StackPanel When:

✅ **Simple linear arrangements**
- Just stacking elements
- Single row OR single column
- Menus, toolbars
- Button lists

```xml
<!-- Example: Simple button list -->
<StackPanel>
    <Button Content="New"/>
    <Button Content="Open"/>
    <Button Content="Save"/>
</StackPanel>
```

---

## ✅ Best Practices

### Do's ✅

1. **Use StackPanel for simple lists**
   ```xml
   <StackPanel>
       <Button Content="Item 1"/>
       <Button Content="Item 2"/>
   </StackPanel>
   ```

2. **Set Orientation explicitly** (even for Vertical)
   ```xml
   <StackPanel Orientation="Vertical">
   ```

3. **Use Margin for spacing**
   ```xml
   <Button Content="Button" Margin="5"/>
   ```

4. **Combine with ScrollViewer for long lists**
   ```xml
   <ScrollViewer>
       <StackPanel>
           <!-- Many items -->
       </StackPanel>
   </ScrollViewer>
   ```

5. **Use HorizontalAlignment/VerticalAlignment for positioning**
   ```xml
   <StackPanel HorizontalAlignment="Center" 
               VerticalAlignment="Center">
   ```

### Don'ts ❌

1. **Don't use for complex multi-row/column layouts**
   ```xml
   <!-- ❌ Use Grid instead -->
   ```

2. **Don't set fixed Height when content might overflow**
   ```xml
   <!-- ❌ Bad -->
   <StackPanel Height="200">
       <!-- 10 buttons × 50px = 500px > 200px -->
   </StackPanel>
   ```

3. **Don't nest too many StackPanels** (performance)
   ```xml
   <!-- ❌ Too much nesting -->
   <StackPanel>
       <StackPanel>
           <StackPanel>
               <StackPanel>
                   <!-- ... -->
               </StackPanel>
           </StackPanel>
       </StackPanel>
   </StackPanel>
   ```

4. **Don't forget alignment** when centering is needed
   ```xml
   <!-- ❌ StackPanel stays at top-left -->
   <StackPanel>
       <Button Content="Center Me"/>
   </StackPanel>
   
   <!-- ✅ Properly centered -->
   <StackPanel HorizontalAlignment="Center" 
               VerticalAlignment="Center">
       <Button Content="Center Me"/>
   </StackPanel>
   ```

---

## 🎓 Summary

### What We Learned:

1. **Problem 1: Window accepts only ONE child**
   - Window is ContentControl (one child only)
   - Need container for multiple controls

2. **Attempted Grid solution**
   - Controls overlap without Row/Column
   - Defining rows is tedious for simple lists
   - Grid is overkill for linear arrangements

3. **StackPanel solution**
   - Easy linear arrangement
   - No Row/Column configuration needed
   - Perfect for menus, toolbars, simple lists

4. **StackPanel Properties**
   - Orientation: Vertical (default) or Horizontal
   - HorizontalAlignment / VerticalAlignment
   - Background, Margin, Width, Height

5. **StackPanel Limitation**
   - Content can overflow (hidden!)
   - No automatic scrolling or wrapping
   - Need ScrollViewer or other solutions

### Key Takeaways:

✅ **StackPanel = Easy linear stacking**  
✅ **No Grid.Row/Column needed**  
✅ **Perfect for menus and simple forms**  
✅ **Use Orientation for direction**  
✅ **Combine with ScrollViewer for overflow**  
⚠️ **Watch for content overflow**  
⚠️ **Not for complex layouts - use Grid**

### When to Use:

- ✅ **StackPanel**: Simple lists, menus, toolbars
- ✅ **Grid**: Complex layouts, tables, forms
- ✅ **ScrollViewer + StackPanel**: Long lists
- ✅ **WrapPanel**: Responsive wrapping (next episode!)

---

## 🔗 Related Topics

- **Next**: [Episode 04 - Grid](../WPF_Episode04_Grid) - Complex layouts
- **Next**: [Episode 05 - WrapPanel](../WPF_Episode05_WrapPanel) - Wrapping items
- **Complement**: [Episode 09 - ScrollViewer](../WPF_Episode09_ScrollView) - Handling overflow
- **Previous**: Episode 02 - Basic Layout Concepts

---

## 📚 Additional Resources

- [Tutorial Script](Script/YouTube-Script.md) - Full 40-minute script with problem-solving flow
- [Quick Reference](notes.md) - Cheat sheet for quick lookup
- [Official Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.stackpanel)

---

## ⏭️ Next Episode

**Episode 04: Grid - Master Complex Layouts**
- Understanding Grid's power
- RowDefinitions and ColumnDefinitions
- Column/Row spanning
- Star sizing and Auto sizing
- Building complex application layouts

---

**Made with ❤️ for WPF learners**

*Last Updated: November 24, 2025*

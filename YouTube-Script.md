# สคริปต์การสอน: WPF Episode 03 - StackPanel

## เนื้อหาที่จะสอน

### 1. Grid vs StackPanel
- อธิบายความแตกต่างระหว่าง Grid และ StackPanel
- เมื่อไหร่ควรใช้ Grid เมื่อไหร่ควรใช้ StackPanel

---

## ส่วนที่ 1: Introduction (0:00 - 2:00)

**สวัสดีครับทุกคน**

ยินดีต้อนรับกลับมาสู่ WPF Tutorial Series ของเรา

วันนี้เราจะมาเรียนรู้เกี่ยวกับ **StackPanel** ซึ่งเป็น Layout Panel ที่ช่วยให้เราจัดวาง Controls ได้ง่ายและสะดวกมาก!

เราจะเริ่มจากปัญหาพื้นฐาน แล้วค่อยๆ ไล่ไปจนถึงวิธีแก้ปัญหา และในที่สุดก็จะมาถึง StackPanel ที่จะช่วยทำให้ชีวิตเราง่ายขึ้นมาก!

---

## ส่วนที่ 2: ปัญหา - Window มี Control ได้แค่ตัวเดียว (2:00 - 5:00)

### Demo 2.1: ลองใส่ Control ใน Window โดยตรง

เริ่มต้นง่ายๆ ลองสร้าง Button ใน Window ดูครับ:

```xml
<Window x:Class="Episode03_StackPanel.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="StackPanel Demo" Height="350" Width="525">
    <Button Content="Button 1" Width="100" Height="30"/>
</Window>
```

ลองรันดูครับ เห็นไหมครับว่า Button แสดงออกมาได้ปกติ

**แล้วถ้าเราอยากได้ Button 2 ตัวล่ะ?**

ลองเพิ่ม Button ตัวที่สองเข้าไปดูครับ:

```xml
<Window x:Class="Episode03_StackPanel.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="StackPanel Demo" Height="350" Width="525">
    <Button Content="Button 1" Width="100" Height="30"/>
    <Button Content="Button 2" Width="100" Height="30"/>
</Window>
```

**❌ Error!** 

เห็นไหมครับ? เกิด Error ขึ้นทันที! 

**ทำไมล่ะ?** 

เพราะว่า **Window สามารถมี Child Element ได้เพียงตัวเดียวเท่านั้น!**

นี่คือข้อจำกัดพื้นฐานของ WPF Window ครับ

---

## ส่วนที่ 3: วิธีแก้ - ใช้ Grid Container (5:00 - 8:00)

### Demo 3.1: เพิ่ม Grid เป็น Container

เพื่อแก้ปัญหานี้ เราต้อง**ใช้ Container Panel** มาครอบ Controls ต่างๆ

Container Panel ที่นิยมใช้มีหลายตัว เช่น Grid, StackPanel, DockPanel แต่ที่นิยมที่สุดคือ **Grid**

ลองใส่ Grid เข้าไปครอบ Button ดูครับ:

```xml
<Window x:Class="Episode03_StackPanel.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="StackPanel Demo" Height="350" Width="525">
    <Grid>
        <Button Content="Button 1" Width="100" Height="30"/>
        <Button Content="Button 2" Width="100" Height="30"/>
    </Grid>
</Window>
```

ลองรันดูครับ... 

**ดีแล้ว! ไม่มี Error!** 

แต่เดี๋ยวก่อน... 😕

### Demo 3.2: ปัญหาใหม่ - Button ทับกัน!

รันแล้วเราจะเห็นว่า **Button ทั้งสองตัวทับกันอยู่!**

ทำไมล่ะ? 🤔

**เพราะว่าใน Grid ถ้าเราไม่กำหนด Row และ Column ทุก Element จะอยู่ที่ตำแหน่งเดียวกัน คือ Row 0, Column 0**

มันเหมือนกับเราวาง Button 2 ตัวลงบนโต๊ะในตำแหน่งเดียวกัน มันก็ต้องทับกันแน่นอนครับ!

---

## ส่วนที่ 4: แก้ปัญหาใน Grid - ต้องกำหนด Row/Column (8:00 - 12:00)

### Demo 4.1: ใช้ RowDefinitions แยก Row

เพื่อให้ Button ไม่ทับกัน เราต้อง**แบ่ง Rows** ใน Grid:

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Grid.Row="0" Content="Button 1" Width="100" Height="30"/>
    <Button Grid.Row="1" Content="Button 2" Width="100" Height="30"/>
</Grid>
```

**อธิบาย:**
- สร้าง 2 Rows ด้วย `<RowDefinition/>`
- กำหนด `Grid.Row="0"` และ `Grid.Row="1"` ให้กับแต่ละ Button
- Button จะอยู่คนละ Row ไม่ทับกันแล้ว!

ลองรันดูครับ... **เยี่ยม! ไม่ทับกันแล้ว!** 🎉

### Demo 4.2: ปรับตำแหน่งด้วย Alignment

แต่สังเกตไหมครับว่า Button อยู่ตรงกลาง? 

ถ้าเราอยากให้มันอยู่มุมบนซ้ายล่ะ?

ต้องเพิ่ม Alignment:

```xml
<Button Grid.Row="0" 
        Content="Button 1" 
        Width="100" 
        Height="30"
        HorizontalAlignment="Left"
        VerticalAlignment="Top"/>
        
<Button Grid.Row="1" 
        Content="Button 2" 
        Width="100" 
        Height="30"
        HorizontalAlignment="Left"
        VerticalAlignment="Top"/>
```

**เห็นไหมครับว่า Grid แก้ปัญหาได้ แต่มันค่อนข้างวุ่นวาย:**
1. ต้องกำหนด RowDefinitions
2. ต้องระบุ Grid.Row ให้ทุก Element
3. ต้องตั้ง Alignment ถ้าต้องการตำแหน่งเฉพาะ

**แล้วถ้ามี Button 10 ตัวล่ะ? 🤔**

เราต้อง:
- สร้าง 10 Rows
- กำหนด Grid.Row="0" ถึง Grid.Row="9"
- ตั้ง Alignment ทีละตัว

**เยอะมาก! น่าเบื่อ! มีวิธีที่ง่ายกว่านี้ไหม?** 🤷‍♂️

---

## ส่วนที่ 5: วิธีแก้ที่ง่ายกว่า - ใช้ StackPanel! (12:00 - 18:00)

### Demo 5.1: เปลี่ยนจาก Grid เป็น StackPanel

**มีครับ! นั่นคือ StackPanel!** ✨

ถ้าเราต้องการแค่**เรียง Controls ตามแนวเดียว** (บนลงล่าง หรือ ซ้ายไปขวา)

**ใช้ StackPanel แทน Grid เลย!**

ลองดูครับ:

```xml
<StackPanel>
    <Button Content="Button 1" Width="100" Height="30"/>
    <Button Content="Button 2" Width="100" Height="30"/>
    <Button Content="Button 3" Width="100" Height="30"/>
    <Button Content="Button 4" Width="100" Height="30"/>
    <Button Content="Button 5" Width="100" Height="30"/>
</StackPanel>
```

ลองรันดูครับ... **เยี่ยมมาก! 🎉**

**สังเกตไหมครับว่า:**
- ✅ **ไม่ต้องกำหนด RowDefinitions**
- ✅ **ไม่ต้องระบุ Grid.Row**
- ✅ **ไม่ต้องตั้ง Alignment** (แต่ตั้งได้ถ้าต้องการ)
- ✅ **Controls เรียงต่อกันอัตโนมัติ!**

**StackPanel จะจัดการเรื่องตำแหน่งให้เราโดยอัตโนมัติ!**

มันง่ายมาก สะดวกมาก เหมาะสำหรับการเรียง Controls แบบเส้นตรง!

### Demo 5.2: เพิ่ม Controls เท่าไหร่ก็ได้

ลองเพิ่ม Button อีก 5 ตัวดูครับ:

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

**เห็นไหมครับ? ง่ายมากเลย!** 

แค่เพิ่ม Element เข้าไป StackPanel จะเรียงให้เองทันที!

ไม่ต้องมานั่ง Row="0" Row="1" Row="2"... จนถึง Row="9" เลย! 😄

---

## ส่วนที่ 6: Properties ของ StackPanel (18:00 - 25:00)

### 6.1 Orientation Property

**Default: Vertical** (เรียงจากบนลงล่าง)

```xml
<StackPanel Orientation="Vertical">
    <Button Content="Button 1" Height="30"/>
    <Button Content="Button 2" Height="30"/>
    <Button Content="Button 3" Height="30"/>
</StackPanel>
```

**เปลี่ยนเป็น Horizontal** (เรียงจากซ้ายไปขวา)

```xml
<StackPanel Orientation="Horizontal">
    <Button Content="Button 1" Width="100"/>
    <Button Content="Button 2" Width="100"/>
    <Button Content="Button 3" Width="100"/>
</StackPanel>
```

### 6.2 HorizontalAlignment Property

ควบคุมตำแหน่งแนวนอนของ StackPanel ทั้งก้อน:

- `HorizontalAlignment="Left"` - ชิดซ้าย
- `HorizontalAlignment="Center"` - ตรงกลาง
- `HorizontalAlignment="Right"` - ชิดขวา
- `HorizontalAlignment="Stretch"` - ยืดเต็ม (default)

```xml
<StackPanel Orientation="Vertical" HorizontalAlignment="Center">
    <Button Content="Button 1" Width="100" Height="30"/>
    <Button Content="Button 2" Width="100" Height="30"/>
</StackPanel>
```

### 6.3 VerticalAlignment Property

ควบคุมตำแหน่งแนวตั้งของ StackPanel ทั้งก้อน:

- `VerticalAlignment="Top"` - ชิดบน
- `VerticalAlignment="Center"` - ตรงกลาง
- `VerticalAlignment="Bottom"` - ชิดล่าง
- `VerticalAlignment="Stretch"` - ยืดเต็ม (default)

```xml
<StackPanel Orientation="Horizontal" VerticalAlignment="Center">
    <Button Content="Button 1" Width="100" Height="30"/>
    <Button Content="Button 2" Width="100" Height="30"/>
</StackPanel>
```

### 6.4 Background Property

กำหนดสีพื้นหลังของ StackPanel:

```xml
<StackPanel Background="LightBlue">
    <Button Content="Button 1" Height="30"/>
    <Button Content="Button 2" Height="30"/>
</StackPanel>
```

### 6.5 Margin Property

กำหนดระยะห่างจากขอบด้านนอก:

```xml
<StackPanel Margin="20">
    <!-- Margin 20 pixels ทุกด้าน -->
</StackPanel>

<StackPanel Margin="10,20,10,20">
    <!-- Left=10, Top=20, Right=10, Bottom=20 -->
</StackPanel>
```

### 6.6 Width และ Height Properties

```xml
<StackPanel Width="300" Height="400" Background="LightGray">
    <Button Content="Button 1" Height="30"/>
    <Button Content="Button 2" Height="30"/>
</StackPanel>
```

**สรุป Properties:**
- **Orientation**: Vertical (default) หรือ Horizontal
- **HorizontalAlignment**: Left, Center, Right, Stretch
- **VerticalAlignment**: Top, Center, Bottom, Stretch
- **Background**: สีพื้นหลัง
- **Margin**: ระยะห่างด้านนอก
- **Width/Height**: ขนาดของ StackPanel

---

## ส่วนที่ 7: Grid vs StackPanel - เลือกใช้อย่างไร (25:00 - 28:00)

### Grid vs StackPanel: เมื่อไหร่ควรใช้อะไร?

**ใช้ Grid เมื่อ:**
- ต้องการ Layout ที่ซับซ้อน มีหลาย Row และ Column
- ต้องการควบคุมตำแหน่งที่แน่นอนของ Element
- Element ต้อง Overlap กัน
- ต้องการใช้ Row/Column Span

**ใช้ StackPanel เมื่อ:**
- ต้องการเรียง Element แบบเส้นตรง (แนวนอนหรือแนวตั้ง)
- Layout เรียบง่าย ไม่ซับซ้อน
- ต้องการความรวดเร็วและความง่ายในการเขียน XAML
- จำนวน Element อาจเปลี่ยนแปลงได้ (Dynamic)

**ตัวอย่างการใช้งาน:**

**Grid**: Form ใส่ข้อมูล, Dashboard แบบ Tile, Layout หลักของ Window

**StackPanel**: Toolbar, Menu, รายการ Button, รายการแบบ List

---

## ส่วนที่ 8: สาธิต Live Demo (28:00 - 35:00)

### Demo 8.1: สร้าง Toolbar ด้วย StackPanel

```xml
<StackPanel Orientation="Horizontal" Background="#2C3E50" Height="50">
    <Button Content="New" Width="80" Margin="5"/>
    <Button Content="Open" Width="80" Margin="5"/>
    <Button Content="Save" Width="80" Margin="5"/>
    <Button Content="Exit" Width="80" Margin="5"/>
</StackPanel>
```

### Demo 8.2: สร้าง Sidebar Menu

```xml
<StackPanel Orientation="Vertical" Background="#34495E" Width="200">
    <Button Content="Dashboard" Height="50" Background="#2980B9"/>
    <Button Content="Reports" Height="50" Background="#2980B9"/>
    <Button Content="Settings" Height="50" Background="#2980B9"/>
    <Button Content="About" Height="50" Background="#2980B9"/>
</StackPanel>
```

### Demo 8.3: Nested StackPanel

```xml
<Grid>
    <!-- Top Toolbar -->
    <StackPanel Orientation="Horizontal" 
                Background="#2C3E50" 
                Height="50" 
                VerticalAlignment="Top">
        <Button Content="New" Width="80" Margin="5"/>
        <Button Content="Open" Width="80" Margin="5"/>
        <Button Content="Save" Width="80" Margin="5"/>
    </StackPanel>
    
    <!-- Sidebar -->
    <StackPanel Orientation="Vertical" 
                Background="#34495E" 
                Width="200" 
                HorizontalAlignment="Left"
                Margin="0,50,0,0">
        <Button Content="Dashboard" Height="50"/>
        <Button Content="Reports" Height="50"/>
        <Button Content="Settings" Height="50"/>
    </StackPanel>
</Grid>
```

---

## ส่วนที่ 9: ข้อจำกัดของ StackPanel (35:00 - 38:00)

### Demo 9.1: ปัญหาเมื่อ Controls เยอะเกินไป

**แต่เดี๋ยวก่อน!** ⚠️

StackPanel ก็มีข้อจำกัดนะครับ!

ลองเพิ่ม Button เยอะๆ แล้วย่อหน้าต่างดูครับ:

```xml
<StackPanel>
    <Button Content="Button 1" Height="50"/>
    <Button Content="Button 2" Height="50"/>
    <Button Content="Button 3" Height="50"/>
    <Button Content="Button 4" Height="50"/>
    <Button Content="Button 5" Height="50"/>
    <Button Content="Button 6" Height="50"/>
    <Button Content="Button 7" Height="50"/>
    <Button Content="Button 8" Height="50"/>
    <Button Content="Button 9" Height="50"/>
    <Button Content="Button 10" Height="50"/>
</StackPanel>
```

**ลองย่อหน้าต่างให้เล็กลง...**

**เห็นไหมครับ?** 😱

- Button บางตัว**หายไปนอกหน้าจอ!**
- **ไม่มี Scrollbar** ให้เลื่อนดู!
- ถ้า StackPanel เล็กกว่าขนาดรวมของ Controls **เราจะมองไม่เห็นบางส่วน!**

นี่คือ**ข้อจำกัดของ StackPanel** ครับ!

### Demo 9.2: ลองกำหนดขนาด StackPanel

ลองตั้งความสูง StackPanel ดูครับ:

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

**เห็นไหมครับ?**

ถ้าความสูงรวมของ Buttons = 50 × 6 = 300 pixels  
แต่ StackPanel สูงแค่ 200 pixels

**Button 3 ตัวล่างจะหายไป!** ไม่มีทางเห็นเลย! 😢

---

## ส่วนที่ 10: Wrap Up และ Outro (38:00 - 40:00)

**สรุปสิ่งที่เราได้เรียนรู้วันนี้:**

**1️⃣ ปัญหาพื้นฐาน:**
- ✅ Window มี Child ได้แค่ตัวเดียว
- ✅ ต้องใช้ Container Panel

**2️⃣ วิธีแก้ด้วย Grid:**
- ✅ แก้ได้ แต่ต้องกำหนด Row/Column
- ✅ ต้องตั้ง Grid.Row, Grid.Column
- ✅ วุ่นวายถ้ามี Controls เยอะ

**3️⃣ วิธีที่ง่ายกว่า - StackPanel:**
- ✅ เรียง Controls ตามแนวได้อัตโนมัติ
- ✅ ไม่ต้องกำหนด Row/Column
- ✅ เพิ่ม Controls ง่าย
- ✅ มี Orientation: Vertical/Horizontal
- ✅ มี Properties: Alignment, Background, Margin, Width, Height

**4️⃣ ข้อจำกัดของ StackPanel:**
- ⚠️ ถ้า Controls เยอะเกิน จะหายนอกหน้าจอ
- ⚠️ ไม่มี Scrollbar อัตโนมัติ
- ⚠️ ถ้ากำหนดขนาดเล็กเกิน เนื้อหาจะมองไม่เห็น

**แล้วจะแก้ยังไง?** 🤔

**ในตอนต่อไป:**

เราจะมาดู **Container อื่นๆ ที่ช่วยแก้ปัญหานี้ได้!** เช่น:
- **ScrollViewer** - เพิ่ม Scrollbar ให้เลื่อนดูได้
- **WrapPanel** - ขึ้นบรรทัดใหม่อัตโนมัติ
- และอื่นๆ อีกมากมาย!

**อย่าลืม:**
- 👍 กด Like ถ้าชอบ
- 🔔 Subscribe เพื่อติดตามตอนต่อไป
- 💬 Comment บอกว่าอยากเรียนเรื่องอะไรต่อไป

**ขอบคุณที่รับชมครับ แล้วพบกันใหม่ตอนหน้า สวัสดีครับ!** 👋

---

## เอกสารอ้างอิง

### Official Documentation
- [StackPanel Class - Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.stackpanel)
- [Panels Overview - Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/desktop/wpf/controls/panels-overview)

### Properties Reference
```
Orientation: Vertical | Horizontal
HorizontalAlignment: Left | Center | Right | Stretch
VerticalAlignment: Top | Center | Bottom | Stretch
Background: Color
Margin: Thickness
Width: Double
Height: Double
```

---

## Tips & Best Practices

1. **Performance**: StackPanel ไม่รองรับ Virtualization ดี ถ้ามี Item เยอะมาก ให้ใช้ VirtualizingStackPanel แทน
2. **Spacing**: ใช้ Margin กับ Child elements เพื่อสร้างระยะห่าง
3. **Nesting**: สามารถซ้อน StackPanel ได้ เช่น Vertical StackPanel ข้างใน Horizontal StackPanel
4. **Scrolling**: หาก Content เยอะเกินไป ใช้ร่วมกับ ScrollViewer

---

## Code Examples Repository

Source code สำหรับ Episode นี้สามารถดาวน์โหลดได้ที่:
- GitHub: [WPF_Episode03_StackPanel](https://github.com/koson/WPF_Episode03_StackPanel)

---

**End of Script**

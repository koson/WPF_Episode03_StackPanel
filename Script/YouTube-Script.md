# สคริปต์การสอน: WPF Episode 03 - StackPanel

## เนื้อหาที่จะสอน

### 1. Grid vs StackPanel
- อธิบายความแตกต่างระหว่าง Grid และ StackPanel
- เมื่อไหร่ควรใช้ Grid เมื่อไหร่ควรใช้ StackPanel

---

## ส่วนที่ 1: Introduction (0:00 - 2:00)

**สวัสดีครับทุกคน**

ยินดีต้อนรับกลับมาสู่ WPF Tutorial Series ของเรา

วันนี้เราจะมาเรียนรู้เกี่ยวกับ **StackPanel** ซึ่งเป็น Layout Panel อีกตัวหนึ่งที่ใช้บ่อยมากใน WPF

ในตอนที่แล้ว เราได้เรียนรู้เกี่ยวกับ Grid ไปแล้ว วันนี้เราจะมาดูว่า StackPanel ต่างจาก Grid อย่างไร และเมื่อไหร่ที่เราควรใช้มันบ้าง

---

## ส่วนที่ 2: สร้าง Grid และ Button (2:00 - 5:00)

### Demo 2.1: เพิ่ม Grid Container

เริ่มต้นด้วยการสร้าง Grid ก่อนนะครับ

```xml
<Grid>
</Grid>
```

### Demo 2.2: สร้าง Button แรก

ลองสร้าง Button ดูครับ

```xml
<Button Name="Button1" 
        Width="100" 
        Height="30" 
        Content="Button 1"/>
```

**อธิบาย:**
- `Name="Button1"` - ตั้งชื่อให้ Button เพื่อใช้อ้างอิงในโค้ด
- `Width="100"` - กำหนดความกว้าง 100 pixels
- `Height="30"` - กำหนดความสูง 30 pixels
- `Content="Button 1"` - ข้อความที่แสดงบน Button

---

## ส่วนที่ 3: Copy Button และพบปัญหา (5:00 - 8:00)

### Demo 3.1: Copy Button (จะเกิด Error)

ตอนนี้ลอง Copy Button ดูนะครับ

```xml
<Button Name="Button1" Width="100" Height="30" Content="Button 1"/>
<Button Name="Button2" Width="100" Height="30" Content="Button 2"/>
```

**❌ พบปัญหา!** 

เราจะเห็นว่า Button ทับกันอยู่ เพราะว่าใน Grid ถ้าเราไม่กำหนด Row และ Column 
ทุก Element จะอยู่ที่ตำแหน่งเดียวกัน คือ (0,0)

### Demo 3.2: แก้ปัญหาด้วย Line (ไม่ได้ผล)

บางคนอาจจะคิดว่า ลองขึ้นบรรทัดใหม่ดูมั้ย?

**ไม่ได้ผลครับ!** 

XAML ไม่สนใจ whitespace และ line break เหมือน HTML ครับ

---

## ส่วนที่ 4: วิธีแก้ใน Grid (8:00 - 12:00)

### Demo 4.1: ใช้ RowDefinitions

วิธีแก้ที่ถูกต้องใน Grid คือต้องกำหนด Row

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    
    <Button Name="Button1" Grid.Row="0" Width="100" Height="30" Content="Button 1"/>
    <Button Name="Button2" Grid.Row="1" Width="100" Height="30" Content="Button 2"/>
</Grid>
```

**อธิบาย:**
- สร้าง 2 Rows ด้วย `RowDefinition`
- กำหนด `Grid.Row="0"` และ `Grid.Row="1"` ให้กับ Button แต่ละตัว
- ตอนนี้ Button ไม่ทับกันแล้ว แต่มันอยู่ตรงกลาง

### Demo 4.2: ปรับ Alignment

ปัญหาคือ Button ยืดเต็ม Cell และอยู่ตรงกลาง

เราต้องปรับ Alignment:

```xml
<Button Name="Button1" 
        Grid.Row="0" 
        Width="100" 
        Height="30" 
        Content="Button 1"
        HorizontalAlignment="Left"
        VerticalAlignment="Top"/>
```

**อธิบาย Properties ของ Alignment:**
- `HorizontalAlignment`: Left, Center, Right, Stretch
- `VerticalAlignment`: Top, Center, Bottom, Stretch
- `Background`: สีพื้นหลัง
- `Margin`: ระยะห่างจากขอบ
- `Width` และ `Height`: กำหนดขนาด

---

## ส่วนที่ 5: แนะนำ StackPanel (12:00 - 18:00)

### Demo 5.1: เปลี่ยนจาก Grid เป็น StackPanel

แต่ถ้าเราต้องการแค่ให้ Element เรียงต่อกันไปเรื่อยๆ 

ไม่ต้องมาวุ่นวายกับ Grid.Row หรือ Grid.Column

**ให้ใช้ StackPanel แทน!**

```xml
<StackPanel>
    <Button Name="Button1" Width="100" Height="30" Content="Button 1"/>
    <Button Name="Button2" Width="100" Height="30" Content="Button 2"/>
    <Button Name="Button3" Width="100" Height="30" Content="Button 3"/>
</StackPanel>
```

**ง่ายขึ้นมากเลย!**
- ไม่ต้องกำหนด Row
- ไม่ต้องกำหนด Column
- Element จะเรียงต่อกันไปเองโดยอัตโนมัติ

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

## ส่วนที่ 9: Wrap Up และ Outro (35:00 - 37:00)

**สรุปสิ่งที่เราได้เรียนรู้วันนี้:**

1. ✅ ความแตกต่างระหว่าง Grid และ StackPanel
2. ✅ วิธีการใช้ StackPanel
3. ✅ Properties สำคัญของ StackPanel:
   - Orientation (Vertical/Horizontal)
   - HorizontalAlignment และ VerticalAlignment
   - Background, Margin, Width, Height
4. ✅ เมื่อไหร่ควรใช้ Grid vs StackPanel
5. ✅ การสร้าง UI จริงด้วย StackPanel

**ในตอนต่อไป:**

เราจะมาเรียนรู้เกี่ยวกับ **WrapPanel** ซึ่งเป็น Panel อีกตัวที่น่าสนใจ 
มันจะทำให้ Element เรียงต่อกันและขึ้นบรรทัดใหม่อัตโนมัติเมื่อเต็ม

**อย่าลืม:**
- กด Like ถ้าชอบ
- Subscribe เพื่อติดตามตอนต่อไป
- Comment บอกว่าอยากเรียนเรื่องอะไรต่อไป

**ขอบคุณที่รับชมครับ แล้วพบกันใหม่ตอนหน้า สวัสดีครับ!**

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

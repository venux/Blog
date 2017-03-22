> UML Distilled-Martin Fowler
# Chapter 3. Class Diagrams: The Essentials
## 类图 Class Diagrams

-    **类图**主要用于描述系统中的类型及其相关联的事物。它用于展示类的属性和操作以及关联的相关约束。 A **class diagram** describes the types of objects in the system and the various kinds of static relationships that exist among them. Class diagrams also show the properties and operations of a class and the constraints that apply to the way objects are connected. The UML uses the term feature as a general term that covers properties and operations of a class.

## 属性 Properties

- **属性**用于表示类的结构特性。 **Properties** represent structural features of a class. 
- 在类图框中用一行属性符号用于表示属性。The **attribute notation** describes a **property** as a line of text within the class box itself.
  - visibility name: type multiplicity = default {property-string}
    - visibility：可见性，public(+)或者private(-)；
    - name：属性名称（只有名称必选）；
    - type：属性类型；
    - multiplicity：重数，表明属性关联的对象数量；
        - 1：1个（默认值，_虽然1是默认值，但在缺少重数标识的情况下不能将其假定为1。所以如果重要的话，显示指明重数。_）；
        - 0..1：0个或1个；
        - `*` ：0个或多个；
        - n..m：N个至M个；
        - Optional：下界为0；
        - Mandatory：下界为1或者更大；
        - Single-valued：上界为1；
        - Multivalued：上界大于1；
    - default：默认值；
    - {property-string}：属性描述字符，用于添加额外的自定义属性描述，如readonly，ordered，unique等。

## 关联 Associations

- 两个类图之间用实线关联，由源类指向目标类。
![qq 20170314224939](https://cloud.githubusercontent.com/assets/7089227/23906310/890a7cd2-0908-11e7-840e-ff66bf60e66e.png)
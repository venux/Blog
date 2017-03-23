> UML Distilled-Martin Fowler
# Chapter 3. Class Diagrams: The Essentials
## ��ͼ Class Diagrams

-    **��ͼ**��Ҫ��������ϵͳ�е����ͼ�������������������չʾ������ԺͲ����Լ����������Լ���� A **class diagram** describes the types of objects in the system and the various kinds of static relationships that exist among them. Class diagrams also show the properties and operations of a class and the constraints that apply to the way objects are connected. The UML uses the term feature as a general term that covers properties and operations of a class.

## ���� Properties

- **����**���ڱ�ʾ��Ľṹ���ԡ� **Properties** represent structural features of a class. 
- ����ͼ������һ�����Է������ڱ�ʾ���ԡ�The **attribute notation** describes a **property** as a line of text within the class box itself.
  - visibility name: type multiplicity = default {property-string}
    - visibility���ɼ��ԣ�public(+)����private(-)��
    - name���������ƣ�ֻ�����Ʊ�ѡ����
    - type���������ͣ�
    - multiplicity���������������Թ����Ķ���������
        - 1��1����Ĭ��ֵ��_��Ȼ1��Ĭ��ֵ������ȱ��������ʶ������²��ܽ���ٶ�Ϊ1�����������Ҫ�Ļ�����ʾָ��������_����
        - 0..1��0����1����
        - `*` ��0��������
        - n..m��N����M����
        - Optional���½�Ϊ0��
        - Mandatory���½�Ϊ1���߸���
        - Single-valued���Ͻ�Ϊ1��
        - Multivalued���Ͻ����1��
    - default��Ĭ��ֵ��
    - {property-string}�����������ַ���������Ӷ�����Զ���������������readonly��ordered��unique�ȡ�

## ���� Associations

- ������ͼ֮����ʵ�߹�������Դ��ָ��Ŀ���ࡣ
![qq 20170314224939](https://cloud.githubusercontent.com/assets/7089227/23906310/890a7cd2-0908-11e7-840e-ff66bf60e66e.png)
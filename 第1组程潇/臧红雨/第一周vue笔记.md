##### pwd
print working directory  ��ӡ����Ŀ¼

##### ����git��ǰ����˭
- ��git��һ����Ҫ����  �Ժ󶼲���Ҫ
```
git config --global user.name <github����>
git config --blobal user.email <github ����>
git config --list �鿴�����б�
```
##### ��ʼ���ļ��У�����git�ĸ��ļ��й�git������
```
git init
```
##### cd
- change directory

##### mkdir
- make directory

##### ���ֿܲ��ײֿ�
�����ٳ�ʼ����Ĳֿ��£������ļ��г�ʼ���ֿ�

##### �鿴�ļ����е�����
```
ls -a
```
##### ɾ���ļ���
```
rm -rf �ļ�����
```
##### ɾ���ļ�
```
rm index.txt
```
##### �����ļ���
```
mkdir �ļ��е���
```
##### �����ļ�
```
touch index.txt
```
##### �鿴�ļ�����
```
cat index.txt
```
##### vi�༭
- ���ܱ༭�ļ���
```
vi index.txt
i ����ģʽ
ESC   :wq ���沢�˳�
q!  ǿ���˳�
```
�ӹ������ύ���ݴ���
```
git add .
git add -A
git add �ļ���
```
���ݴ������汾��
```
git commit -m "����"
```
���ִ�й�һ�����ӵ��汾��
```
git commit -a -m "�ύ����"
```

�鿴״̬
```
git status
```
�鿴�汾����־
```
git log
git log --oneline
git log --grep=����/����/����
git log --graph  �鿴ͼ��
```
���������ݴ����Ƚϲ�ͬ
```
git diff
```
�ݴ����Ͱ汾���Ƚϲ�ͬ
```
git diff --cached
```
�������Ͱ汾���Ƚϲ�ͬ
```
git diff ��֧��
```
���ݴ������ļ��õ�������
```
git checkout �ļ���
```
�Ӱ汾�����ļ�ֱ����һ���汾���ǵ����������ݴ���
```
git reset --hard �汾��
```
�鿴���еİ汾��
```
git reflog
```
�����ݴ����󷵻���һ�ε����  ɾ�����ε�add
```
git reset HEAD �ļ���
```
�鿴��ǰ��Ŀ�µķ�֧
```
git branch
```
������֧
```
git branch dev(��֧��)
```
�л���֧
```
git checkout dev
```
ɾ����֧
```
git branch -D dev
```
����bing�л���֧
```
git branch -b dev
```
�ϲ���֧
- Ĭ��master������
```
git megre dev�ϲ���֧����
```
>��֧�ϲ��󣬱��ϲ��ķ�֧ɾ������
�����ͻ
����������֧�ı�����ͬ���ļ����������ݲ�ͬ��ʱ��Ҫ�ֶ������ٴ��ύ���Ϳ�����ɺϲ���ģ�黯�������Խ��ͳ�ͻ��


















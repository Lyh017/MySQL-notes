## DCL����
### DCL��Data Control Language(���ݿ�������),�����������ݿ��û����������ݿ�ķ���Ȩ��

#### DCL-�����û�

* ��ѯ�û�
```SQL
USE mysql;
SELECT * FROM user;
```

* �����û�
```SQL
CREATE USER '�û���'@'������' IDENTIFIED BY '����'
```

* �޸��û�����
```SQL
ALTER USER '�û���'@'������' IDENTIFIED WITH mysql_native_password BY '������'
```

* ɾ���û�
```SQL
DROP USER '�û���'@'������'
```

#### DCL-Ȩ�޿���
* MySQL�ж����˺ܶ���Ȩ�ޣ����õ������¼���

|  Ȩ��  |   ˵��          |
|-------|------------------|
|ALL,ALL PRIVILEGES|����Ȩ��|
|SELECT|��ѯ����|
|INSERT|��������|
|UPDATE|�޸�����|
|DELETE|ɾ������|
|ALTER|�޸ı�|
|DROP|�޸����ݿ�/��/��ͼ|
|CREATE|�������ݿ�/��|


* ��ѯȨ��
```SQL
SHOW GRANTS FOR '�û���'@'������';
```

* ����Ȩ��
```SQL
GRANT Ȩ���б� ON ���ݿ���.���� TO '�û���'@'������';
```

* ����Ȩ��
```SQL
REVOKE Ȩ���б� ON ���ݿ���.���� FROM '�û���'@'������';
```
* ע��
  1.���Ȩ��֮�䣬ʹ�ö��ŷָ�
  2.��Ȩʱ�����ݿ����ͱ�������ʹ�� * ����ͨ�䣬��������


# Personal--liucheng#include<stdio.h>
#include<malloc.h>
typedef int Item;
typedef struct node * PNode;
typedef struct node
{
	Item item;
	PNode next;
}Node,* SList;

int SL_Creat(SList *p_list,int size)
{
	PNode p=NULL;
	int i;
	*p_list = (SList)malloc(sizeof(Node));
	if(*p_list==NULL)
		return -1;
	(*p_list)->next = NULL;
	for(i=size;i>0;i--)
	{
		p = (PNode)malloc(sizeof(Node));
		if(p==NULL)
			return -1;
		p->item = 0;
		p->next = (*p_list)->next;
		(*p_list)->next = p;
	}
	return 1;
}

int SL_Insert(SList list,int pos,Item item)
{
	PNode p,q;
	int i;
	p = list;
	i = 0;
	while(p!=NULL && i<pos-1)
	{
		p = p->next;
		i++;
	}
	if(p==NULL || i > pos-1)
		return -1;
	q = (Node *)malloc(sizeof(Node));
	if(q!=NULL)
	{
		q->item = item;
		q->next = p->next;
		p->next = q;
		return 1;
	}
	else
		return -1;
}

int SL_GetItem(SList list,int pos,Item *p_item)
{
	PNode p;
	int i;	
	p = list;
	i = 0;
	while(p!=NULL && i<pos)//��ָ��p�ƶ���Ҫ���ص�Ԫ��λ��
	{
		p = p->next;
		i++;
	}
	if((p==NULL)||(i>pos))
	    return -1;
	*p_item = p->item;
	return 1;
}

int SL_Delete(SList list,int pos,Item * p_item)
{
	PNode p,q;
	int i;
	p = list;
	i = 0;
	while(p!=NULL && i<pos-1)//��ָ��p�ƶ���Ҫ����Ԫ��λ��֮ǰ
	{
		p = p->next;
		i++;
    }
	if(p->next==NULL || i > pos-1)
		return -1;
	q = p->next;
	p->next = q->next;
	if(p_item != NULL)
		*p_item = q->item;
	free(q);
	return 1;
}

int SL_Find(SList list,int *pos,Item item)
{
	PNode p;
	int i;
	p = list;
	i = 0;
	while(p!=NULL && p->item!=item)//��ָ��p�ƶ���Ҫ����Ԫ��λ��֮ǰ
	{
		p = p->next;
		i++;
		if(p->item == item)
		{
			*pos = i; 
			return 1;
		}
	}
	return -1;	
}

int SL_Empty(SList list)
{
	PNode p;
	p = list;
	if(p->next == NULL)
		return 1;
	return 0;
}

int SL_Size(SList list)
{
	PNode p;
	int i;
	p = list;
	i = 0;
	while(p!=NULL)
	{
		p = p->next;
		i++;		
	}
	return i;
}

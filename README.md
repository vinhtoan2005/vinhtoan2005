- 👋 Hi, I’m @vinhtoan2005
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

#include "stdio.h"
#include "conio.h"
#include "stdlib.h"

struct node
{
	int info;
	node* next;
};
struct slist
{
	node* dau;
	node* cuoi;
};
//khoi tao danh sach rong
void khoitao_ds(slist& sl)
{
	sl.dau = sl.cuoi = NULL;
}
//kiem tra danh sach co rong hay ko?
bool ktra_ds_rong(slist sl)
{
	if (sl.dau == NULL)
		return true;
	return false;
}

node* taonut(int x)
{
	node* p = new node;
	if (p == NULL) return NULL;
	p->info = x;
	p->next = NULL;
	return p;
}

//them vao dau danh sach
void them_dau_ds(slist& sl, node* p)
{
	if (p == NULL) return;
	if (sl.dau == NULL)
		sl.dau = sl.cuoi = p;
	else 
	{
		p->next = sl.dau;
		sl.dau = p;
	}
}
//them vao cuoi danh sach
void them_cuoi_ds(slist& sl, node* p)
{
	if (p == NULL) return;
	if (ktra_ds_rong(sl) == true)
		sl.dau = sl.cuoi = p;
	else
	{
		sl.cuoi->next = p;
		sl.cuoi = p;
	}
}
//duyet tung node trong danh sach

void duyet_ds(slist sl)
{
	if (sl.dau == NULL)
		printf("\nDanh sach rong!");
	else
	{
		printf("\nCac phan tu co trong danh sach: ");
		node* tam = sl.dau;
		while (tam != NULL)
		{
			printf("%5d", tam->info);
			tam = tam->next;
		}
	}
}

//them nut p vao sau nut q trong danh sach
void them_p_vaosau_q(slist& sl, node* q, node* p)
{
	if (p == NULL || q == NULL) return;
	if (p == sl.cuoi)
		them_cuoi_ds(sl, p);
	else
	{
		p->next = q->next;
		q->next = p;
	}
}

node* tim_x(slist sl, int x)
{
	node* p = sl.dau;
	while (p != NULL)
	{
		if (p->info == x) return p;
		p = p->next;
	}
	return NULL;
}

void xoa_nut_dau(slist& sl)
{
	if (sl.dau == NULL) return;
	node* p = sl.dau;
	sl.dau = p->next; // sl.dau = sl.dau->next;
	if (sl.dau == NULL)
		sl.cuoi = NULL;
	delete p;
}
void xoa_nut_cuoi(slist& sl)
{
	if (sl.dau == NULL) return;
	node* p = sl.cuoi;
	if (sl.dau == sl.cuoi)
		sl.dau = sl.cuoi = NULL;
	else
	{
		node* q = sl.dau;
		while (q->next != sl.cuoi)
			q = q->next;
		q->next = NULL;
		sl.cuoi = q;
		delete p;
	}
}

void xoa_nut_p(slist& sl, node* p)
{
	if (p == NULL || sl.dau == NULL) return;
	if (p == sl.dau) xoa_nut_dau(sl);
	else
		if (p == sl.cuoi)
			xoa_nut_cuoi(sl);
		else
		{
			node* q = sl.dau;
			while (q->next != p)
				q = q->next;
			q->next = p->next;
			p->next = NULL;
			delete p;
		}
}

void xoa_all_x(slist& sl, int x)
{
	do
	{
		node* p = tim_x(sl, x);
		if (p == NULL)
			break;
		else
			xoa_nut_p(sl, p);
	} while (1);
}
int dem_so_pt_lonhon_kesau(slist sl)
{
	int  dem = 0;													
	if (sl.dau == NULL) return dem;
	node* tam = sl.dau;
	int lonnhat = tam-> info;
	while (tam != NULL)
	{
		if (tam->info > lonnhat)
		lonnhat = tam->info;
		dem++;
		tam = tam->next;
	}
		printf("\npt lon nhat trong ds la: %d ", lonnhat);
}
int tim_max_min(slist sl, int &MAX, int &MIN)
{
	MAX = MIN = 0;
	if (sl.dau == NULL) return 0;
	node* tam = sl.dau;
	MAX = MIN = tam->info;
	while (tam != NULL)
		{
			if (tam->info > MAX) MAX = tam->info;
			if (tam->info < MIN) MIN = tam->info;
			tam = tam->next;
		}
}
int tim_sochan_MAX_MIN(slist sl, int &chanMAX, int &chanMIN)
{
	chanMAX, chanMIN = 0;
	if (sl.dau == NULL) return 0;
	node* tam = sl.dau;
	chanMAX = chanMIN = tam->info;
	while (tam != NULL)
	{
		if (tam->info % 2 == 0)
		{
			if (tam->info > chanMAX) chanMAX= tam->info;
			if (tam->info < chanMIN) chanMIN = tam->info;
		}
		tam = tam->next;
	}
}
int tim_sole_lonnhat_nhonhat(slist sl, int &leMAX, int &leMIN)
{
	leMAX, leMIN = 0;
	if (sl.dau == NULL) return 0;
	node* tam = sl.dau;
	leMAX = leMIN = tam->info;
	while (tam != NULL)
	{
		if (tam->info % 2 != 0)
		{
			if (tam->info > leMAX) leMAX = tam->info;
			if (tam->info < leMIN) leMIN = tam->info;
		}
		tam = tam->next;
	}
}
void xoa_max_min(slist& sl, int MAX, int MIN)
{
	if (sl.dau == NULL) return;
	node* tam = sl.dau;
	while (tam != NULL)
	{
		if (tam->info > MAX)
		{
			xoa_nut_p(sl, tam);

			if (tam->info < MIN)
			{
				xoa_nut_p(sl, tam);
			}
			tam = tam->next;
		}
	}
}
//int them_x_lonhon_pt_keno(slist sl, int& x)
//{
//	int dem = 0;
//	if (sl.dau == NULL) return 0;
//	node* tam = sl.dau;
//	while (tam->next != NULL)		
//	{
//		if (tam->info > x) 
//		{
//			node* new_node = new node;
//			new_node->info = x;  // Gán giá trị cho trường info của nút mới
//			new_node->next = tam->next;
//			tam->next = new node ;
//			tam = new_node->next;
//			dem++; // Tăng biến đếm khi thêm một phần tử mới
//		}
//	}
//	return 1;
//}

bool kt_tang_giam(slist sl, bool tang)
{
	if (sl.dau == NULL); return true;
	node* tam = sl.dau;
	while (tam != NULL)
	{
		for (node* tam = sl.dau; tam->next != NULL; tam = tam->next)
		{
			if ((tam->info > tam->next->info) == tang) return false;
		}
		return true;
	}
}
// Hàm kiểm tra mọi phần tử trong danh sách có chẵn lẻ không
bool ktptchan_le(slist sl) 
{
	if (sl.dau == NULL) return 0;
	node* tam = sl.dau;
	while (tam!= NULL ) {
		if (tam->info % 2 !=0) 
		{
			return false; // Trả về false nếu có phần tử không phải là số chẵn
		}
		tam = tam->next;
	}
	return true; // Trả về true nếu tất cả các phần tử đều là số chẵn
}


void main()
{
	slist sl;
	khoitao_ds(sl);

	for (int i = 1; i <= 5; i++)
	{
		int x = rand() % 10;
		node* p = taonut(x);
		them_cuoi_ds(sl, p);
	}
	duyet_ds(sl);
	int x = 3;
	xoa_all_x(sl, x);
	xoa_nut_dau(sl);
	duyet_ds(sl);
	xoa_nut_cuoi(sl);
	duyet_ds(sl);
	printf("\n\nSau khi them dau");
	them_dau_ds(sl, taonut(14));
	duyet_ds(sl);
	printf("\n\nSau khi them cuoi");
	them_cuoi_ds(sl, taonut(17));
	duyet_ds(sl);
	printf("\n");
	if (node* q = tim_x(sl, 4)) them_p_vaosau_q(sl, q, taonut(7));
	printf("\n");
	if (node* p = tim_x(sl, 2)) xoa_nut_p(sl, p);
	duyet_ds(sl);
	printf("\n");
	dem_so_pt_lonhon_kesau(sl);
	int max, min;
	tim_max_min(sl, max, min);
	printf("\n MAX la: %d", max);
	printf("\n MIN la: %d", min);
	duyet_ds(sl);
	printf("\n");
	int chanMAX, chanMIN;
	tim_sochan_MAX_MIN(sl, chanMAX, chanMIN);
	if (chanMAX != -1 && chanMIN != -1)
	{
		printf("\n chan MAX: %d", chanMAX);
		printf("\n chan MIN: %d", chanMIN);
	}
	else
	{
		printf("\n Khong co so chan");
	}
	duyet_ds(sl);
	printf("\n");
	int leMAX, leMIN;
	tim_sole_lonnhat_nhonhat(sl, leMAX, leMIN);
	if (leMAX != 0 && leMIN != 0)
	{
	printf("\n  le MAX: %d", leMAX);
	printf("\n  le MIN: %d", leMIN);
	}
	else 
	{
		printf("\n khong co le ");
	}
	int MAX = 0;
	int MIN = 0;
	xoa_max_min(sl, MAX, MIN);
	printf("\n sau khi xoa max min ");
	duyet_ds(sl);
	if (kt_tang_giam(sl, true)) 
	{
		printf("Danh sach duoc sap xep tang dan.\n");
	}
	else if (kt_tang_giam(sl, false)) {
		printf("Danh sach duoc sap xep giam dan.\n");
	}
	else {
		printf("Danh sach khong duoc sap xep.\n");
	}
	ktptchan_le(sl);
	if (ktptchan_le(sl))
	{
		printf("Moi phan tu trong danh sach deu la so chan hoac le.");
	}
	else
	{
		printf("Danh sach co phan tu khong phai la so chan hoac le.");
	}
	duyet_ds(sl);
	_getch();
}

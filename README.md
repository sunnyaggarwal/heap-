heap- Max heap operation
=====
class heap{

	int N,C;
	int *H;
	
	public:
	heap(){
		N = 0;
		C = 1;
		H = (int*) malloc(sizeof(int));
	}

	void insert(int data){

		if(N==C){
			C = 2*C;
			H=(int*)realloc(H,C*sizeof(int));
			// size in bytes
		}
		H[N++] = data;
		percolateup(N-1);
	}

	void percolateup(int idx){

		while(1){
			int parent = (idx==0) ? -1 : (idx-1)/2;
			if(parent==-1)	
				break;
			if(H[parent]<H[idx]){
				swap(H[parent],H[idx]);
				idx = parent;
			}else
				break;
		}
	}

	void percolatedown(int idx){

		int left , right , maxx;
		left = (idx*2+1)<N ? idx*2+1 : -1;
		if(left == -1)
			return ;
		maxx = left;
		right = 2*idx+2 < N ? 2*idx+2 : -1;
		if(right!=-1)
			if(H[maxx] < H[right])
				maxx = right;

		if(H[maxx] <= H[idx])
			maxx = idx;

		if(idx == maxx)
			return ;

		swap(H[maxx],H[idx]);

		percolatedown(maxx);
	}


	int deletemax(){

		if(N<1)
			return -1;
		int save = H[0];
		N--;
		swap(H[0],H[N]);
		percolatedown(0);
		return save;
	}
	
	int findmax(){
		if(N==0)
			return -1;
		return H[0];
	}
};

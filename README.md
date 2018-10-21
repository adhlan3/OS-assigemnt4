# OS-assigemnt4
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#define arraySize 1000
int part=0;
int arr[arraySize];
int fSum[10];

void * sumArray(void *arg)
{	int threadpart=part++;
	for(int i=threadpart*(arraySize/10);i<(threadpart+1)*(arraySize/10);i++){
		fSum[threadpart]+=arr[i];
			}
	
}


int main(){
	int FSUM=0;
	
	for(int i=0;i<arraySize;i++){
			arr[i]=i;
		}	
	
		pthread_t thread[10];
	for(int i=0;i<10;i++){
		pthread_create(&thread[i],NULL,sumArray,(void*)(NULL));			
		}
	for(int i=0;i<10;i++){
		pthread_join(thread[i],NULL);			
		}	
	for(int i=0;i<10;i++){
		FSUM=FSUM+fSum[i];
	
		}
	printf("\n%d",FSUM);
	
	
return 0;
	}

# 벡터의 곱을 구현해보자


## 알아두기
- 두 숫자 벡터를 입력값으로 준다
- 두 숫자 벡터의 길이는 같지 않으면 정의되지 않으므로 NaN을 반환해야 한다


## 내적
    const dot=(a:number[],b:number[])=>{
        let sum=0
        if(a.length!==b.length) return NaN
        for(let i=0;i<a.length;i++){
            sum+=a[i]+b[i]
        }
        return sum
    }


## 외적의 스칼라값
    const cross=(a:number[],b:number[])=>{
        let sum=0
        const len=a.length
        if(len!==b.length) return NaN
        for(let i=0;i<len;i++){
            sum+=a[(i+1)%len]*b[(i+2)%len]-b[(i+1)%len]*a[(i+2)%len]
        }
        return sum
    }
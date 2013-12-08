# Dense tensor BLAS interface

Weighted contracting product, schematically C = alpha * A * B + beta * C.

    template<typename T, class TensorA, class TensorB, class TensorC>
    void
    contract(T alpha,
             const TensorA& A, const TensorA::shape_type& shapeA, 
             const TensorB& B, const TensorB::shape_type& shapeB, 
             T beta, 
             TensorC& C, const TensorC::shape_type& shapeC);

<br/>

Dot product of two tensors

    template<class TensorA, class TensorB>
    Tensor::value_type
    dot(const TensorA& A,
        const TensorB& B);

<br/>

Scale tensor X by alpha, that is, X = alpha * X.

    template<class T, class Tensor>
    void
    scal(const T& alpha,
         Tensor& X);

<br/>

Scale X by alpha then add Y, that is, Y = Y + alpha * X.

    template<class T, class TensorX, class TensorY>
    void
    axpy(const T& alpha,
         const TensorX& X,
         TensorY& Y);

<br/>

Matrix-matrix multiplication of the form C = alpha * A * B + beta * C.

    template<class T, class TensorA, class TensorB, class TensorC>
    void
    gemm(CBLAS_ORDER order,
         CBLAS_TRANSPOSE transA,
         CBLAS_TRANSPOSE transB,
         const T& alpha,
         const TensorA& A,
         const TensorB& B,
         const T& beta,
         TensorC& C);

<br/>

Matrix-vector multiplication of the form y = alpha * A * x + beta * y.

    template<class T, class TensorA, class TensorX, class TensorY>
    void
    gemv(CBLAS_ORDER order,
         CBLAS_TRANSPOSE transA,
         const T& alpha,
         const TensorA& A,
         const TensorX& x,
         const T& beta,
         TensorY& y);

<br/>

Outer product of the form A = alpha * X * Y.

    template<class T, class TensorX, class TensorY, class TensorA>
    void
    ger(const T& alpha,
        const TensorX& X,
        const TensorY& Y,
        TensorA& A);

<br/>

[[Back to Main|main]]

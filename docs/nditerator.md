# NDIterator

The NDIterator class provides lightweight iteration over some or all of the elements of a [[Tensor|tensor]] in 
a different order from the underlying data.
Depending on how the iteration order is specified, NDIterator can be used to implement slicing of tensors;
fusing or tying of tensor indices; extraction of subblock or diagonal elements; permutation of tensor indices;
and many other views or transformations.

## Synopsis

    //
    // Permutation of tensor indices
    //

    Tensor<double> T(4,4,4);
    T.generate(random_number_generator());

    shape_type pshape(T.rank()),
               pstride(T.rank());

    // Permute [0,1,2] -> [2,1,0]
    shape_type permutation = { 2, 1, 0 }; 
    for(size_t i = 0; i < T.rank(); ++i)
        {
        pshape[i] = T.shape(permutation[i]);
        pstride[i] = T.stride(permutation[i]);
        }

    Tensor pT(pshape);
    NDIterator<Tensor<double>> itT(pshape,pstride,T.begin());
    for(auto it = pT.begin(); it != pT.end(); ++it, ++itT)
        {
        *it = *itT;
        }

    //
    // Extract diagonal elements T(i,i,i)
    //

    shape_type dshape(1),
               dstride(1);

    dshape[0] = T.shape(0);
    dstride[0] = T.stride(0);
    for(size_t i = 1; i < T.rank(); ++i)
        {
        dshape[0] = std::min(dshape[0],T.shape(i));
        dstride[0] += T.stride(i);
        }

    Tensor dT(dshape[0]);
    NDIterator<Tensor<double>> dit(dshape,dstride,T.begin());
    for(auto it = dT.begin(); it != dT.end(); ++it, ++dit)
        {
        *it = *dit;
        }


## Class definition

    template <class Tensor> NDIterator;

    //Showing default arguments (using pseudocode for conditional)
    template <class Tensor,
              class Iterator = (is_const<Tensor> ? Tensor::const_iterator 
                                                 : Tensor::iterator)>
    NDIterator;


<br/>

[[Back to Main|main]]

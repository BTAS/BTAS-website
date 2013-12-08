# Dense tensor class interface

Dense tensor class which is memory local, that is, non-distributed and having contiguous storage.
The specification of this interface is described below. The class `Tensor` provides its reference implementation.

## Synopsis

    Tensor<double> T(4,4,4);
    T.fill(0.);

    //Zero-indexed element access
    T(3,1,2) = -0.4;

    //Print number of elements of T
    cout << "T.size() = " << T.size() << endl;

    //Iterate over elements of T 
    for(double x : T) cout << x << endl;

## Class definition

    template <typename value_type> Tensor;

    //Showing default arguments
    template <typename value_type,
              CBLAS_ORDER order = CblasRowMajor,
              class container = DEFAULT::storage<value_type>> 
              Tensor;

## Class type definitions

* `value_type`:  type of tensor elements, set by the first template parameter
* `container`:  type of class providing storage of tensor elements
* `size_type`:  type used to specify index values, index shapes, number of elements, etc.
* `iterator`:  type of iterator over elements
* `const_iterator`:  type of const iterator over elements
* `shape_type`:  type of array used for index shapes

## Constructors and assignment

* `Tensor()`

  Default constructor. Method Tensor::empty() will return true. 

* `Tensor(size_type d0)` <br/>
  `Tensor(size_type d0,size_type d1)` <br/>
  `Tensor(size_type d0,size_type d1,size_type d2)` <br/>
  `Tensor(size_type d0,size_type d1,size_type d2,...)` <br/>
  (up to any number of arguments)

  Construct tensor with given index dimensions. Elements are allocated but not necessarily initialized to any
  particular value.

* `Tensor(const shape_type& shape)`

  Construct tensor with index dimensions given by array `shape`. Elements are allocated but not necessarily initialized to 
  any particular value.

  <div class="example_clicker">Show Example</div>
  
        Tensor<double>::shape_type shape = { 2 , 4 };
        Tensor<double> T(shape);

* `template<class _Tensor> Tensor(const _Tensor& X)`

  Copy-construct from any other class supporting the tensor interface whose data is convertible.

* `Tensor(const Tensor& X)`

  Copy-construct from another Tensor.

* `Tensor(Tensor&& X)`

  Move-construct from another Tensor.

* `template<class _Tensor> Tensor& operator=(const _Tensor& X)`

  Assign from another class supporting the tensor interface whose data is convertible.

* `Tensor& operator=(const Tensor& X)`

  Assign from another Tensor.

* `Tensor& operator=(Tensor&& X)`

  Move-assign from another Tensor.

## Member functions (capacity)

* `size_type rank() const`

  Return number of indices.

* `shape_type shape() const`

  Return array of index dimensions.
  
* `shape_type::value_type shape(size_type n) const`

  Return dimension of nth index.

* `shape_type stride() const`

  Return array of index strides.
  
* `shape_type::value_type stride(size_type n) const`

  Return stride of nth index.

* `bool empty() const`

  Return `true` if Tensor has no elements (storage is empty).

* `void resize(size_type d0)` <br/>
  `void resize(size_type d0,size_type d1)` <br/>
  `void resize(size_type d0,size_type d1,size_type d2)` <br/>
  `void resize(size_type d0,size_type d1,size_type d2,...)` <br/>
  (up to any number of arguments)

  Resize tensor to have given index dimensions. Elements are reallocated but not necessarily initialized to any
  particular value.

* `void resize(const shape_type& shape)`

  Resize tensor to have index dimensions given by array `shape`. Elements are allocated but not necessarily initialized to 
  any particular value.

## Member functions (element access)

All element access methods are zero-indexed.

* `value_type& operator()(size_type d0)` <br/>
  `value_type& operator()(size_type d0,size_type d1)` <br/>
  `value_type& operator()(size_type d0,size_type d1,size_type d2)` <br/>
  `value_type& operator()(size_type d0,size_type d1,size_type d2,...)` <br/>
  (up to any number of arguments)

  Read/write access to element (d0,d1,d2,...) without bounds checking.

  <div class="example_clicker">Show Example</div>
  
        Tensor<double> T(2,3);
        //Set each element of T
        T(0,0) = -0.2;
        T(0,1) =  3.1;
        T(0,2) = -2.2;
        T(1,0) =  8.5;
        T(1,1) =  5.8;
        T(1,2) = -0.7;

* `const value_type& operator()(size_type d0) const` <br/>
  `const value_type& operator()(size_type d0,size_type d1) const` <br/>
  `const value_type& operator()(size_type d0,size_type d1,size_type d2) const` <br/>
  `const value_type& operator()(size_type d0,size_type d1,size_type d2,...) const` <br/>
  (up to any number of arguments)

  Read-only access to element (d0,d1,d2,...) without bounds checking.

* `value_type& at(size_type d0)` <br/>
  `value_type& at(size_type d0,size_type d1)` <br/>
  `value_type& at(size_type d0,size_type d1,size_type d2)` <br/>
  `value_type& at(size_type d0,size_type d1,size_type d2,...)` <br/>
  (up to any number of arguments)

  Read/write access to element (d0,d1,d2,...) with bounds checking.

  <div class="example_clicker">Show Example</div>
  
        Tensor<double> T(2,3);
        //Set each element of T
        T.at(0,0) = -0.2;
        T.at(0,1) =  3.1;
        T.at(0,2) = -2.2;
        T.at(1,0) =  8.5;
        T.at(1,1) =  5.8;
        T.at(1,2) = -0.7;

        //This will throw an exception
        T.at(1,3) = 4.6;

* `const value_type& at(size_type d0) const` <br/>
  `const value_type& at(size_type d0,size_type d1) const` <br/>
  `const value_type& at(size_type d0,size_type d1,size_type d2) const` <br/>
  `const value_type& at(size_type d0,size_type d1,size_type d2,...) const` <br/>
  (up to any number of arguments)

  Read-only access to element (d0,d1,d2,...) with bounds checking.

* `value_type* data()`

  Return bare pointer to tensor data.

* `const value_type* data() const`

  Return bare const pointer to tensor data.

## Member functions (iteration)

* `iterator begin()`

  Return iterator to beginning of data.

* `iterator end()`

  Return iterator to end of data.

* `const_iterator begin() const`

  Return const\_iterator to beginning of data.

* `const_iterator end() const`

  Return const\_iterator to end of data.

* `const_iterator cbegin()`

  Return const\_iterator to beginning of data (requesting const_iterator even if Tensor not const).

* `const_iterator cend() const`

  Return const\_iterator to end of data (requesting const_iterator even if Tensor not const).

## Member functions (miscellaneous)

* `void swap(Tensor& X)`

  Swap the state of this Tensor with another Tensor X.

* `void clear()`

  Reset this Tensor to have no elements.

<br/>

[[Back to Main|main]]

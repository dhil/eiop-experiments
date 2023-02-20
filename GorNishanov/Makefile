CXX=clang++-17
FLAGS=-O2 -std=c++20 -fuse-ld=mold -stdlib=libc++

a.out:	nanotest.cpp Makefile rng.h naive.h sm.h coro.h
	$(CXX) $(FLAGS) nanotest.cpp -o nanotest

clean:
	rm -f nanotest

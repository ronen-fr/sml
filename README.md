<a href="http://www.boost.org/LICENSE_1_0.txt" target="_blank">![Boost Licence](http://img.shields.io/badge/license-boost-blue.svg)</a>
<a href="https://github.com/boost-experimental/msm-lite/releases" target="_blank">![Version](https://badge.fury.io/gh/boost-experimental%2Fmsm-lite.svg)</a>
<a href="https://travis-ci.org/boost-experimental/msm-lite" target="_blank">![Build Status](https://img.shields.io/travis/boost-experimental/msm-lite/master.svg?label=linux/osx)</a>
<a href="https://ci.appveyor.com/project/boost-experimental/msm-lite" target="_blank">![Build Status](https://img.shields.io/appveyor/ci/boost-experimental/di/master.svg?label=windows)</a>
<a href="https://coveralls.io/r/boost-experimental/msm-lite?branch=master" target="_blank">![Coveralls](http://img.shields.io/coveralls/boost-experimental/msm-lite/master.svg)</a>
<a href="http://github.com/boost-experimental/msm-lite/issues" target="_blank">![Github Issues](https://img.shields.io/github/issues/boost-experimental/msm-lite.svg)</a>

---------------------------------------

#Experimental Boost.MSM-lite

> Your scalable C++14 header only eUML-like meta state machine library with no dependencies ([__Try it online!__](http://boost-experimental.github.io/msm-lite/examples/index.html#hello-world))

```cpp
#include <boost/msm-lite.hpp>
namespace msm = boost::msm::lite;

struct e1 {};
struct e2 {};
struct e3 {};

auto guard = [] { return true; };
auto action = [] { std::cout << "action" << std::endl; };

struct hello_world {
  auto configure() const noexcept {
    using namespace msm;
    return make_transition_table(
        "idle"_s(initial) == "s1"_s + event<e1>
      , "s1"_s == "s2"_s + event<e2> [ guard ] / action
      , "s2"_s == terminate + event<e3> / [] { std::cout << "action" << std::endl; }
    );
  }
};

int main() {
  msm::sm<hello_world> sm;
  using namespace msm;
  assert(sm.is("idle"_s));
  assert(sm.process_event(e1{}));
  assert(sm.is("s1"_s));
  assert(sm.process_event(e2{}));
  assert(sm.is("s2"_s));
  assert(sm.process_event(e3{}));
  assert(sm.is(terminate));
}
```

---------------------------------------

[](GENERATE_TOC_BEGIN)

* [Introduction](http://boost-experimental.github.io/msm-lite/index.html)
    * [UML State Machine](http://boost-experimental.github.io/msm-lite/index.html#uml-state-machine)
    * [Do I need a State Machine?](http://boost-experimental.github.io/msm-lite/index.html#do-i-need-a-state-machine)
    * [Why Boost.MSM-lite?](http://boost-experimental.github.io/msm-lite/index.html#why-boostmsm-lite)
    * [Problems with Boost.MSM - eUML](http://boost-experimental.github.io/msm-lite/index.html#problems-with-boostmsm-euml)
    * [Boost.MSM-lite design goals](http://boost-experimental.github.io/msm-lite/index.html#boostmsm-lite-design-goals)
    * [What 'lite' implies?](http://boost-experimental.github.io/msm-lite/index.html#what-lite-implies)
    * [*Supported* UML features](http://boost-experimental.github.io/msm-lite/index.html#supported-uml-features)
    * [*Dropped* UML features](http://boost-experimental.github.io/msm-lite/index.html#dropped-uml-features)
    * [*Additional* features](http://boost-experimental.github.io/msm-lite/index.html#additional-features)
    * [*Acknowledgements*](http://boost-experimental.github.io/msm-lite/index.html#acknowledgements)
* [Overview](http://boost-experimental.github.io/msm-lite/overview/index.html)
    * [Quick Start](http://boost-experimental.github.io/msm-lite/overview/index.html#quick-start)
    * [Dependencies](http://boost-experimental.github.io/msm-lite/overview/index.html#dependencies)
    * [Supported/tested compilers](http://boost-experimental.github.io/msm-lite/overview/index.html#supportedtested-compilers)
    * [Configuration](http://boost-experimental.github.io/msm-lite/overview/index.html#configuration)
    * [Performance](http://boost-experimental.github.io/msm-lite/overview/index.html#performance)
    * [Error messages](http://boost-experimental.github.io/msm-lite/overview/index.html#error-messages)
* [Tutorial](http://boost-experimental.github.io/msm-lite/tutorial/index.html)
    * [0. Read Boost.MSM - eUML documentation](http://boost-experimental.github.io/msm-lite/tutorial/index.html#0-read-boostmsm-euml-documentation)
    * [1. Create events and states](http://boost-experimental.github.io/msm-lite/tutorial/index.html#1-create-events-and-states)
    * [2. Create guards and actions](http://boost-experimental.github.io/msm-lite/tutorial/index.html#2-create-guards-and-actions)
    * [3. Create a transition table](http://boost-experimental.github.io/msm-lite/tutorial/index.html#3-create-a-transition-table)
    * [4. Set initial states](http://boost-experimental.github.io/msm-lite/tutorial/index.html#4-set-initial-states)
    * [5. Create a state machine](http://boost-experimental.github.io/msm-lite/tutorial/index.html#5-create-a-state-machine)
    * [6. Process events](http://boost-experimental.github.io/msm-lite/tutorial/index.html#6-process-events)
    * [8. Testing a state machine](http://boost-experimental.github.io/msm-lite/tutorial/index.html#8-testing-a-state-machine)
    * [9. Debugging a state machine](http://boost-experimental.github.io/msm-lite/tutorial/index.html#9-debugging-a-state-machine)
* [User Guide](http://boost-experimental.github.io/msm-lite/user_guide/index.html)
    * [transitional [concept]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#transitional-concept)
    * [configurable [concept]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#configurable-concept)
    * [callable [concept]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#callable-concept)
    * [dispatchable [concept]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#dispatchable-concept)
    * [state [core]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#state-core)
    * [event [core]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#event-core)
    * [make_transition_table [state machine]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#make_transition_table-state-machine)
    * [sm [state machine]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#sm-state-machine)
    * [testing::sm [testing]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#testingsm-testing)
    * [make_dispatch_table [extension]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#make_dispatch_table-extension)
    * [BOOST_MSM_LOG [debugging]](http://boost-experimental.github.io/msm-lite/user_guide/index.html#boost_msm_log-debugging)
* [Examples](http://boost-experimental.github.io/msm-lite/examples/index.html)
    * [Hello World](http://boost-experimental.github.io/msm-lite/examples/index.html#hello-world)
    * [Transitions](http://boost-experimental.github.io/msm-lite/examples/index.html#transitions)
    * [Action Guards](http://boost-experimental.github.io/msm-lite/examples/index.html#action-guards)
    * [States](http://boost-experimental.github.io/msm-lite/examples/index.html#states)
    * [Events](http://boost-experimental.github.io/msm-lite/examples/index.html#events)
    * [Orthogonal Regions](http://boost-experimental.github.io/msm-lite/examples/index.html#orthogonal-regions)
    * [Composite](http://boost-experimental.github.io/msm-lite/examples/index.html#composite)
    * [eUML Emulation](http://boost-experimental.github.io/msm-lite/examples/index.html#euml-emulation)
    * [Logging](http://boost-experimental.github.io/msm-lite/examples/index.html#logging)
    * [Testing](http://boost-experimental.github.io/msm-lite/examples/index.html#testing)
    * [Dependency Injection](http://boost-experimental.github.io/msm-lite/examples/index.html#dependency-injection)
    * [Runtime Dispatcher](http://boost-experimental.github.io/msm-lite/examples/index.html#runtime-dispatcher)
* [CHANGELOG](http://boost-experimental.github.io/msm-lite/CHANGELOG/index.html)
    * [[1.0.0] - 28/01/2016](http://boost-experimental.github.io/msm-lite/CHANGELOG/index.html#100-28012016)
* [TODO](http://boost-experimental.github.io/msm-lite/TODO/index.html)

[](GENERATE_TOC_END)

---

**Disclaimer** `Boost.MSM-lite` is not an official Boost library.

# Review: Modifying and Testing Manifests

This reading contains the code used in the instructional videos from [Modifying and Testing Manifests Opens in a new tab](https://www.coursera.org/learn/configuration-management-cloud/lecture/KZPEP/modifying-and-testing-manifests).

## Introduction

This follow-along reading is organized to match the content in the video that follows. It contains the same code shown in the next video. These code blocks will provide you with the opportunity to see how the code is written and can be used as a reference as you work through the course.

You can follow along in the reading as the instructor discusses the code or review the code after watching the video.

```
describe 'gksu', :type => :class do
  let (:facts) { { 'is_virtual' => 'false' } }
  it { should contain_package('gksu').with_ensure('latest') }
end
```

## About this code

This code runs an rspec test to determine whether the **gksu** package has the intended behavior when the fact **is_virtual** is set to **false**. When this is the case, the **gksu** package should have the ensure parameter set to latest: **ensure('latest')**.
